.. _doc_rigid_body:

Sử dụng RigidBody
=================

Vật thể cứng là gì?
-------------------

Vật thể cứng là vật thể được physics engine điều khiển trực tiếp để mô phỏng hành vi của các đối tượng vật lý. Để xác định hình dạng của vật thể, bạn phải gán một hoặc nhiều đối tượng :ref:`Shape3D <class_Shape3D>` cho nó. Lưu ý rằng việc thiết lập vị trí của các hình dạng này sẽ ảnh hưởng đến tâm khối lượng của vật thể.

Cách điều khiển vật thể cứng
----------------------------

Bạn có thể thay đổi hành vi của vật thể cứng bằng cách thiết lập các thuộc tính của nó, chẳng hạn như khối lượng và trọng lượng. Cần thêm một physics material vào vật thể cứng để điều chỉnh độ ma sát và độ nảy, cũng như thiết lập xem nó có khả năng hấp thụ và/hoặc thô ráp hay không. Bạn có thể thiết lập các thuộc tính này trong Inspector hoặc thông qua code. Xem :ref:`RigidBody3D <class_RigidBody3D>` và :ref:`PhysicsMaterial <class_PhysicsMaterial>` để biết danh sách đầy đủ các thuộc tính và tác động của chúng.

Có một số cách để điều khiển chuyển động của vật thể cứng, tùy thuộc vào mục đích sử dụng của bạn.

Nếu bạn chỉ cần đặt một vật thể cứng một lần, chẳng hạn như để thiết lập vị trí ban đầu, bạn có thể sử dụng các phương thức do node :ref:`Node3D <class_Node3D>` cung cấp, chẳng hạn như ``set_global_transform()`` hoặc ``look_at()``. Tuy nhiên, bạn không thể gọi các phương thức này ở mỗi frame, nếu không physics engine sẽ không thể mô phỏng chính xác trạng thái của vật thể. Ví dụ, hãy xem xét một vật thể cứng mà bạn muốn xoay để hướng về phía một đối tượng khác. Một lỗi phổ biến khi triển khai kiểu hành vi này là sử dụng ``look_at()`` ở mỗi frame, khiến mô phỏng vật lý bị lỗi. Dưới đây, chúng ta sẽ trình bày cách triển khai đúng.

Việc bạn không thể sử dụng các phương thức ``set_global_transform()`` hoặc ``look_at()`` không có nghĩa là bạn không thể toàn quyền điều khiển một vật thể cứng. Thay vào đó, bạn có thể điều khiển nó bằng callback ``_integrate_forces()``. Trong phương thức này, bạn có thể thêm *lực*, áp dụng *xung lực* hoặc thiết lập *vận tốc* để đạt được bất kỳ chuyển động nào bạn mong muốn.

Phương thức "look at"
---------------------

Như đã mô tả ở trên, không thể sử dụng phương thức ``look_at()`` của Node3D ở mỗi frame để bám theo một mục tiêu. Dưới đây là một phương thức ``look_at()`` tùy chỉnh có tên ``look_follow()``, hoạt động với các vật thể cứng:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends RigidBody3D

    var speed: float = 0.1

    func look_follow(state: PhysicsDirectBodyState3D, current_transform: Transform3D, target_position: Vector3) -> void:
        var forward_local_axis: Vector3 = Vector3(1, 0, 0)
        var forward_dir: Vector3 = (current_transform.basis * forward_local_axis).normalized()
        var target_dir: Vector3 = (target_position - current_transform.origin).normalized()
        var local_speed: float = clampf(speed, 0, acos(forward_dir.dot(target_dir)))
        if forward_dir.dot(target_dir) > 1e-4:
            state.angular_velocity = local_speed * forward_dir.cross(target_dir) / state.step

    func _integrate_forces(state):
        var target_position = $my_target_node3d_node.global_transform.origin
        look_follow(state, global_transform, target_position)

 .. code-tab:: csharp

    using Godot;

    public partial class MyRigidBody3D : RigidBody3D
    {
        private float _speed = 0.1f;
        private void LookFollow(PhysicsDirectBodyState3D state, Transform3D currentTransform, Vector3 targetPosition)
        {
            Vector3 forwardLocalAxis = new Vector3(1, 0, 0);
            Vector3 forwardDir = (currentTransform.Basis * forwardLocalAxis).Normalized();
            Vector3 targetDir = (targetPosition - currentTransform.Origin).Normalized();
            float localSpeed = Mathf.Clamp(_speed, 0.0f, Mathf.Acos(forwardDir.Dot(targetDir)));
            if (forwardDir.Dot(targetDir) > 1e-4)
            {
                state.AngularVelocity = forwardDir.Cross(targetDir) * localSpeed / state.Step;
            }
        }

        public override void _IntegrateForces(PhysicsDirectBodyState3D state)
        {
            Vector3 targetPosition = GetNode<Node3D>("MyTargetNode3DNode").GlobalTransform.Origin;
            LookFollow(state, GlobalTransform, targetPosition);
        }
    }


Phương thức này sử dụng thuộc tính ``angular_velocity`` của vật thể cứng để xoay vật thể. Trục xoay được xác định bởi tích có hướng giữa hướng tiến hiện tại và hướng mà vật thể cần nhìn tới. ``clamp`` là một phương thức đơn giản được dùng để ngăn lượng xoay vượt quá hướng cần nhìn tới, vì tổng lượng xoay cần thiết được xác định bởi arccosine của tích vô hướng. Phương thức này cũng có thể được sử dụng với ``axis_lock_angular_*``. Nếu cần kiểm soát chính xác hơn, có thể cần đến các giải pháp như những giải pháp dựa trên :ref:`class_Quaternion`, như đã thảo luận trong :ref:`doc_using_transforms`.

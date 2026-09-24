.. _doc_navigation_different_actor_locomotion:

Hỗ trợ các kiểu di chuyển khác nhau của actor
=============================================

.. image:: img/nav_actor_locomotion.png

Để hỗ trợ các kiểu di chuyển khác nhau của actor như cúi người và bò, cần có thiết lập bản đồ tương tự như khi hỗ trợ :ref:`doc_navigation_different_actor_types`.

Bake các navigation mesh khác nhau với chiều cao phù hợp cho actor đang cúi người hoặc bò, để chúng có thể tìm đường đi qua những khu vực hẹp đó trong thế giới game của bạn.

Khi actor thay đổi trạng thái di chuyển, chẳng hạn như đứng lên, bắt đầu cúi người hoặc bò, hãy truy vấn bản đồ thích hợp để tìm đường đi.

Nếu hành vi tránh né cũng cần thay đổi theo trạng thái di chuyển, chẳng hạn như chỉ tránh khi đang đứng hoặc chỉ tránh các agent khác ở cùng trạng thái di chuyển, hãy chuyển avoidance agent của actor sang một avoidance map khác sau mỗi lần thay đổi trạng thái di chuyển.

.. tabs::
 .. code-tab:: gdscript GDScript

    func update_path():

        if actor_standing:
            path = NavigationServer3D.map_get_path(standing_navigation_map_rid, start_position, target_position, true)
        elif actor_crouching:
            path = NavigationServer3D.map_get_path(crouched_navigation_map_rid, start_position, target_position, true)
        elif actor_crawling:
            path = NavigationServer3D.map_get_path(crawling_navigation_map_rid, start_position, target_position, true)

    func change_agent_avoidance_state():

        if actor_standing:
            NavigationServer3D.agent_set_map(avoidance_agent_rid, standing_navigation_map_rid)
        elif actor_crouching:
            NavigationServer3D.agent_set_map(avoidance_agent_rid, crouched_navigation_map_rid)
        elif actor_crawling:
            NavigationServer3D.agent_set_map(avoidance_agent_rid, crawling_navigation_map_rid)

 .. code-tab:: csharp

    private void UpdatePath()
    {
        if (_actorStanding)
        {
            _path = NavigationServer3D.MapGetPath(_standingNavigationMapRid, _startPosition, _targetPosition, true);
        }
        else if (_actorCrouching)
        {
            _path = NavigationServer3D.MapGetPath(_crouchedNavigationMapRid, _startPosition, _targetPosition, true);
        }
        else if (_actorCrawling)
        {
            _path = NavigationServer3D.MapGetPath(_crawlingNavigationMapRid, _startPosition, _targetPosition, true);
        }
    }

    private void ChangeAgentAvoidanceState()
    {
        if (_actorStanding)
        {
            NavigationServer3D.AgentSetMap(_avoidanceAgentRid, _standingNavigationMapRid);
        }
        else if (_actorCrouching)
        {
            NavigationServer3D.AgentSetMap(_avoidanceAgentRid, _crouchedNavigationMapRid);
        }
        else if (_actorCrawling)
        {
            NavigationServer3D.AgentSetMap(_avoidanceAgentRid, _crawlingNavigationMapRid);
        }
    }

.. note::

    Mặc dù có thể thực hiện truy vấn đường đi ngay lập tức cho nhiều map, việc chuyển map của avoidance agent sẽ chỉ có hiệu lực sau lần đồng bộ hóa máy chủ tiếp theo.

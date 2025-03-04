:tocdepth: 3

policy/frameworks/management/controller/api.zeek
================================================
.. zeek:namespace:: Management::Controller::API

The event API of cluster controllers. Most endpoints consist of event pairs,
where the controller answers a zeek-client request event with a
corresponding response event. Such event pairs share the same name prefix
and end in "_request" and "_response", respectively.

:Namespace: Management::Controller::API
:Imports: :doc:`policy/frameworks/management/types.zeek </scripts/policy/frameworks/management/types.zeek>`

Summary
~~~~~~~
Constants
#########
=================================================================== ================================================================
:zeek:id:`Management::Controller::API::version`: :zeek:type:`count` A simple versioning scheme, used to track basic compatibility of
                                                                    controller, agents, and zeek-client.
=================================================================== ================================================================

Events
######
====================================================================================== ======================================================================
:zeek:id:`Management::Controller::API::get_instances_request`: :zeek:type:`event`      zeek-client sends this event to request a list of the currently
                                                                                       peered agents/instances.
:zeek:id:`Management::Controller::API::get_instances_response`: :zeek:type:`event`     Response to a get_instances_request event.
:zeek:id:`Management::Controller::API::get_nodes_request`: :zeek:type:`event`          zeek-client sends this event to request a list of
                                                                                       :zeek:see:`Management::NodeStatus` records that capture
                                                                                       the status of Supervisor-managed nodes running on the cluster's
                                                                                       instances.
:zeek:id:`Management::Controller::API::get_nodes_response`: :zeek:type:`event`         Response to a get_nodes_request event.
:zeek:id:`Management::Controller::API::notify_agents_ready`: :zeek:type:`event`        The controller triggers this event when the operational cluster
                                                                                       instances align with the ones desired by the cluster
                                                                                       configuration.
:zeek:id:`Management::Controller::API::set_configuration_request`: :zeek:type:`event`  zeek-client sends this event to establish a new cluster configuration,
                                                                                       including the full cluster topology.
:zeek:id:`Management::Controller::API::set_configuration_response`: :zeek:type:`event` Response to a set_configuration_request event.
:zeek:id:`Management::Controller::API::test_timeout_request`: :zeek:type:`event`       This event causes no further action (other than getting logged) if
                                                                                       with_state is F.
:zeek:id:`Management::Controller::API::test_timeout_response`: :zeek:type:`event`      Response to a test_timeout_request event.
====================================================================================== ======================================================================


Detailed Interface
~~~~~~~~~~~~~~~~~~
Constants
#########
.. zeek:id:: Management::Controller::API::version
   :source-code: policy/frameworks/management/controller/api.zeek 13 13

   :Type: :zeek:type:`count`
   :Default: ``1``

   A simple versioning scheme, used to track basic compatibility of
   controller, agents, and zeek-client.

Events
######
.. zeek:id:: Management::Controller::API::get_instances_request
   :source-code: policy/frameworks/management/controller/main.zeek 463 478

   :Type: :zeek:type:`event` (reqid: :zeek:type:`string`)

   zeek-client sends this event to request a list of the currently
   peered agents/instances.
   

   :reqid: a request identifier string, echoed in the response event.
   

.. zeek:id:: Management::Controller::API::get_instances_response
   :source-code: policy/frameworks/management/controller/api.zeek 31 31

   :Type: :zeek:type:`event` (reqid: :zeek:type:`string`, result: :zeek:type:`Management::Result`)

   Response to a get_instances_request event. The controller sends
   this back to the client.
   

   :reqid: the request identifier used in the request event.
   

   :result: the result record. Its data member is a
       :zeek:see:`Management::Instance` record.
   

.. zeek:id:: Management::Controller::API::get_nodes_request
   :source-code: policy/frameworks/management/controller/main.zeek 524 556

   :Type: :zeek:type:`event` (reqid: :zeek:type:`string`)

   zeek-client sends this event to request a list of
   :zeek:see:`Management::NodeStatus` records that capture
   the status of Supervisor-managed nodes running on the cluster's
   instances.
   

   :reqid: a request identifier string, echoed in the response event.
   

.. zeek:id:: Management::Controller::API::get_nodes_response
   :source-code: policy/frameworks/management/controller/api.zeek 79 79

   :Type: :zeek:type:`event` (reqid: :zeek:type:`string`, result: :zeek:type:`Management::ResultVec`)

   Response to a get_nodes_request event. The controller sends this
   back to the client.
   

   :reqid: the request identifier used in the request event.
   

   :result: a :zeek:type`vector` of :zeek:see:`Management::Result`
       records. Each record covers one cluster instance. Each record's data
       member is a vector of :zeek:see:`Management::NodeStatus`
       records, covering the nodes at that instance. Results may also indicate
       failure, with error messages indicating what went wrong.

.. zeek:id:: Management::Controller::API::notify_agents_ready
   :source-code: policy/frameworks/management/controller/main.zeek 209 228

   :Type: :zeek:type:`event` (instances: :zeek:type:`set` [:zeek:type:`string`])

   The controller triggers this event when the operational cluster
   instances align with the ones desired by the cluster
   configuration. It's essentially a cluster management readiness
   event. This event is currently only used by the controller and not
   published to other topics.
   

   :instances: the set of instance names now ready.
   

.. zeek:id:: Management::Controller::API::set_configuration_request
   :source-code: policy/frameworks/management/controller/main.zeek 352 462

   :Type: :zeek:type:`event` (reqid: :zeek:type:`string`, config: :zeek:type:`Management::Configuration`)

   zeek-client sends this event to establish a new cluster configuration,
   including the full cluster topology. The controller processes the update
   and relays it to the agents. Once each has responded (or a timeout occurs)
   the controller sends a corresponding response event back to the client.
   

   :reqid: a request identifier string, echoed in the response event.
   

   :config: a :zeek:see:`Management::Configuration` record
       specifying the cluster configuration.
   

.. zeek:id:: Management::Controller::API::set_configuration_response
   :source-code: policy/frameworks/management/controller/api.zeek 56 56

   :Type: :zeek:type:`event` (reqid: :zeek:type:`string`, result: :zeek:type:`Management::ResultVec`)

   Response to a set_configuration_request event. The controller sends
   this back to the client.
   

   :reqid: the request identifier used in the request event.
   

   :result: a vector of :zeek:see:`Management::Result` records.
       Each member captures one agent's response.
   

.. zeek:id:: Management::Controller::API::test_timeout_request
   :source-code: policy/frameworks/management/controller/main.zeek 603 614

   :Type: :zeek:type:`event` (reqid: :zeek:type:`string`, with_state: :zeek:type:`bool`)

   This event causes no further action (other than getting logged) if
   with_state is F. When T, the controller establishes request state, and
   the controller only ever sends the response event when this state times
   out.
   

   :reqid: a request identifier string, echoed in the response event when
       with_state is T.
   

   :with_state: flag indicating whether the controller should keep (and
       time out) request state for this request.
   

.. zeek:id:: Management::Controller::API::test_timeout_response
   :source-code: policy/frameworks/management/controller/api.zeek 104 104

   :Type: :zeek:type:`event` (reqid: :zeek:type:`string`, result: :zeek:type:`Management::Result`)

   Response to a test_timeout_request event. The controller sends this
   back to the client if the original request had the with_state flag.
   

   :reqid: the request identifier used in the request event.
   



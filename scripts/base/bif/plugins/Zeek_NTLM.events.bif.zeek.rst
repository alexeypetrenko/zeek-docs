:tocdepth: 3

base/bif/plugins/Zeek_NTLM.events.bif.zeek
==========================================
.. zeek:namespace:: GLOBAL


:Namespace: GLOBAL

Summary
~~~~~~~
Events
######
================================================ ============================================================================
:zeek:id:`ntlm_authenticate`: :zeek:type:`event` Generated for :abbr:`NTLM (NT LAN Manager)` messages of type *authenticate*.
:zeek:id:`ntlm_challenge`: :zeek:type:`event`    Generated for :abbr:`NTLM (NT LAN Manager)` messages of type *challenge*.
:zeek:id:`ntlm_negotiate`: :zeek:type:`event`    Generated for :abbr:`NTLM (NT LAN Manager)` messages of type *negotiate*.
================================================ ============================================================================


Detailed Interface
~~~~~~~~~~~~~~~~~~
Events
######
.. zeek:id:: ntlm_authenticate
   :source-code: base/protocols/ntlm/main.zeek 86 96

   :Type: :zeek:type:`event` (c: :zeek:type:`connection`, request: :zeek:type:`NTLM::Authenticate`)

   Generated for :abbr:`NTLM (NT LAN Manager)` messages of type *authenticate*.
   

   :c: The connection.
   

   :request: The parsed data of the :abbr:`NTLM (NT LAN Manager)` message. See init-bare for more details.
   
   .. zeek:see:: ntlm_negotiate ntlm_challenge

.. zeek:id:: ntlm_challenge
   :source-code: base/protocols/ntlm/main.zeek 70 84

   :Type: :zeek:type:`event` (c: :zeek:type:`connection`, challenge: :zeek:type:`NTLM::Challenge`)

   Generated for :abbr:`NTLM (NT LAN Manager)` messages of type *challenge*.
   

   :c: The connection.
   

   :negotiate: The parsed data of the :abbr:`NTLM (NT LAN Manager)` message. See init-bare for more details.
   
   .. zeek:see:: ntlm_negotiate ntlm_authenticate

.. zeek:id:: ntlm_negotiate
   :source-code: base/protocols/ntlm/main.zeek 65 68

   :Type: :zeek:type:`event` (c: :zeek:type:`connection`, negotiate: :zeek:type:`NTLM::Negotiate`)

   Generated for :abbr:`NTLM (NT LAN Manager)` messages of type *negotiate*.
   

   :c: The connection.
   

   :negotiate: The parsed data of the :abbr:`NTLM (NT LAN Manager)` message. See init-bare for more details.
   
   .. zeek:see:: ntlm_challenge ntlm_authenticate



:tocdepth: 3

base/bif/plugins/Zeek_File.events.bif.zeek
==========================================
.. zeek:namespace:: GLOBAL


:Namespace: GLOBAL

Summary
~~~~~~~
Events
######
=============================================== ========================================================================
:zeek:id:`file_transferred`: :zeek:type:`event` Generated when a TCP connection associated w/ file data transfer is seen
                                                (e.g.
=============================================== ========================================================================


Detailed Interface
~~~~~~~~~~~~~~~~~~
Events
######
.. zeek:id:: file_transferred
   :source-code: base/protocols/ftp/main.zeek 339 347

   :Type: :zeek:type:`event` (c: :zeek:type:`connection`, prefix: :zeek:type:`string`, descr: :zeek:type:`string`, mime_type: :zeek:type:`string`)

   Generated when a TCP connection associated w/ file data transfer is seen
   (e.g. as happens w/ FTP or IRC).
   

   :c: The connection over which file data is transferred.
   

   :prefix: Up to 1024 bytes of the file data.
   

   :descr: Deprecated/unused argument.
   

   :mime_type: MIME type of the file or "<unknown>" if no file magic signatures
              matched.



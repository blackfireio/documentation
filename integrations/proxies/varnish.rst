Varnish
=======

As described in the :doc:`reverse proxies documentation
section </up-and-running/reverse-proxies>`, you need to bypass Varnish when
profiling. You can do this in your VCL file, based on the sample below.

VCL Sample
----------

.. code-block:: vcl

    acl profile {
       # Authorized IPs, add your own IPs from which you want to profile.
       "x.y.z.w";

       # Add the Blackfire.io IPs when using builds:
       # Ref https://docs.blackfire.io/reference-guide/faq#how-should-i-configure-my-firewall-to-let-blackfire-access-my-apps
       "46.51.168.2";
       "54.75.240.245";
    }

    sub vcl_recv {
      if (req.esi_level > 0) {
        # ESI request should not be included in the profile.
        # Instead you should profile them separately, each one
        # in their dedicated profile.
        # Removing the Blackfire header avoids to trigger the profiling.
        # Not returning let it go trough your usual workflow as a regular
        # ESI request without distinction.
        unset req.http.X-Blackfire-Query;
      }

      # If it's a Blackfire query and the client is authorized,
      # just pass directly to the application.
      if (req.http.X-Blackfire-Query && client.ip ~ profile) {
        return (pass);
      }
    }

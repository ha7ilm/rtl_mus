rtl_mus
=======

**RTL Multi-User Server** is a small python script to allow multiple clients control the same RTL-SDR compatible DVB-T tuner, while also receiving I/Q samples.

> As of 2020-05-27, this project is not developed anymore. Check the `nmux` tool in [csdr](https://github.com/ha7ilm/csdr) for a faster alternative (however, that does not support forwarding commands, so it's not an exact replacement).

## How does it work?
- <tt>rtl\_mus</tt> requires an instance of <tt>rtl\_tcp</tt> to connect to. 
- When it receives a command from any of its clients, <tt>rtl\_mus</tt> resends it to the <tt>rtl\_tcp</tt> server. 
- It continously reads samples from <tt>rtl\_tcp</tt>, and resends them to the clients.

## Other features

###  DSP processing

<tt>rtl\_mus</tt> can also execute a command to perform DSP processing on the I/Q stream; then the processed I/Q stream is sent to its clients. 
A sample command for FLAC processing is included in the config file. FLAC is a loseless codec originally intended for audio, but it seems to work on sampled RF, too... :smile: As of a FLAC processed I/Q stream requires about 20% less bandwidth than the original, it might help to transport I/Q signals over a low-bandwidth internet link, but as of none of the SDR software can decode FLAC right now, another instance of <tt>rtl\_mus</tt> has to be run locally, to decode the FLAC-encoded signal. 


### Permissions on commands
By changing the source code, one can easily allow and deny remote clients execute particular commands on the <tt>rtl\_tcp</tt> server. Commands that are not allowed are simply not forwarded by <tt>rtl\_mus</tt>.

### On rtl_tcp crash it fills clients with zeros 
It can be particularly useful to avoid your GNU Radio flowgraph hang when using an OsmoSDR Source block.

## Authors

András Retzler 
<ha7ilm@sdr.hu>

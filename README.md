# munin-livebox-monitor
A really basic plug-in to monitor, in munin, the Livebox (3&amp;4) DSL rates wich are set by a certain Orange's _Dynamic Line Management_ service.<br>
It relies on @rene-d [sysbus](https://github.com/rene-d/sysbus) project to connect and grab datas.
I added this code into [sysbus.py](https://github.com/rene-d/sysbus/blob/master/sysbus.py) to get simpler data for the plugin.<br>
```
def dslrate2_cmd(args):
        """ DSL datarate for munin"""
        result = requete("NeMo.Intf.data:getMIBs", { "traverse":"down", "mibs":"dsl" })
        if 'status' in result and 'dsl' in result['status'] and 'dsl0' in result['status']['dsl']:
            m = result['status']['dsl']['dsl0']
            print(m['DownstreamCurrRate'] * 0.88)
            print(m['UpstreamCurrRate'] * 0.88)
        else:
            print("DSL rate non disponible")
```

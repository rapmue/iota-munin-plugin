# iota-munin-plugin
This munin plugin is useful to monitor the transactions of your neighbors over time.

## Requirements
The plugins use the shell command `jq` which you will find at https://stedolan.github.io/jq/.

## Installation
To install just link the two bash files in your `/etc/munin/plugins/` folder and restart `munin-node`.

After the plugin is enabled and munin run at least once, there should be a section called iota in your munin overview.

Have fun.

## Detailed instructions
You can setup a munin-master and/or a munin-node. The master collects the data from all nodes and visualizes them. If you want you can setup just one master and multiple nodes or setup the master and node on every machine you want to monitor.

You will find detailed instructions on how to install a master or node for your corresponding system [here](http://guide.munin-monitoring.org/en/latest/installation/install.html).

After installing the node, you have to select which plugins you want to use. You can get a list of plugins and the corresponding softlink commands to activate them with `munin-node-configure --shell`. For more information on how to configure a plugin visit the original [documentation](http://guide.munin-monitoring.org/en/latest/plugin/use.html#plugin-use).

After activating plugins you have to restart the munin-node service. Otherwise the plugins won't work.

To test your plugin you can use `munin-run yourplugin` and you'll get the output of your plugin directly in your console.

On your node you have to allow the master to connect. Usually this is configured in the file `/etc/munin/munin-node.conf`. Also make sure to open the port set in the node configuration on your firewall (Usually port 4949).

On your master you have to add your node. Usually this is configured in the file `/etc/munin/munin.conf`. If you have multiple nodes, the nodes are grouped by your domains or node names. ([Original docs](http://guide.munin-monitoring.org/en/latest/installation/configuration.html#add-some-nodes))

I use something like this:

```
[server1.example.com]
    address 127.0.0.1
    use_node_name yes
[server2.example.com]
    address 10.0.0.4
    use_node_name yes
```

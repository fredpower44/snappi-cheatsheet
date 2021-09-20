
# **snappi** Cheat-Sheet Guide
 ![](https://github.com/open-traffic-generator/snappi/raw/main/snappi-logo.png)
  **https://github.com/open-traffic-generator/snappi** |
| --- |

# Creating config

| **Code template** | **example** |
| --- | --- |
| `api = snappi.api()cfg = api.config()` | `api = snappi.api() cfg = api.config()` |
|` api = snappi.api(ext='ixnetwork') cfg = api.config()` | `api = snappi.api(ext='trex') cfg = api.config()` |

# Adding Ports/flows (or other snappi list objects)

| **Code template** | **example** |
| --- | --- |
| `cfg.ports.port().port().port()...` | `p1, p2 = cfg.ports.port(name='p1').port(name='p2')` |
| `cfg.flows.flow().flow().flow()...` | `f2 = cfg.flows.flow(name='f1').flow(name='f2')[-1]` |
| `cfg.ports.add()` | `p3 = cfg.ports.add(name='p3')` |
| `cfg.flows.add()` | `f3 = cfg.flows.add(name='f3')` |
| `cfg.ports.append({port object})` | `p4 = p3.clone(); p4.name = 'p4'cfg.ports.append(p4)` |
| `cfg.flows.append({flow object})` | `f4 = f3.clone(); f3.name = 'f4'cfg.flows.append(f4)` |

# ACCESSING Ports/flows (or other snappi list objects)

| **Code template** | **example** |
| --- | --- |
| `a, b, c ... = cfg.ports # or cfg.flows` | `p1, p2, p3 = cfg.ports` |
| `a = cfg.ports[-1] # or cfg.flows` | `flow = cfg.flows [-1]` |

# Removing Ports/FLOWS (OR OTHER SNAPPI LIST OBJECTS)

| **Code template** | **example** |
| --- | --- |
| `cfg.ports.remove({index})` | `cfg.ports.port(name='p0').port(name='p1').port(name='p2')`<br>`cfg.ports.remove(2) # Removes p2` |
| cfg.flows.remove({index}) | cfg.flows.remove(0) **# Removes first flow** |
| cfg.ports.clear() | cfg.ports.clear() **# Removes all ports** |
| cfg.flows.clear() | cfg.flows.clear() **# Removes all flows** |

# Configuring FLows

| **Code template** | **example** |
| --- | --- |
| {flow}.tx\_rx.port.tx\_name = {port name} | **# flow f1 will transmit from port p1** f1.tx\_rx.port.tx\_name = 'p1' |
| {flow}.tx\_rx.port.rx\_name = {port name} | **# port p2 will receive from flow f1** f1.tx\_rx.port.rx\_name = 'p2' |
| {flow}.size.fixed = {packet size} | **# flow f1 will send packets of fixed size 256 bytes** f1.size.fixed = 256 |
| {flow}.duration.fixed\_packets.packets = {num packets} | **# flow f1 will send 1000 packets** f1.duration.fixed\_packets.packets = 1000 |
| {flow}.rate.pps = {packets per second} | **# flow f1 will transmit at 100 packets per second** f1.rate.pps = 100 |

# Creating packets

| **Code template** | **example** |
| --- | --- |
| {flow}.packet.ethernet().ipv4().udp() | **# flow f1 will transmit ethernet/ipv4/udp packets** eth1,ip1,udp1 = f1.packet.ethernet().ipv4().udp() |
| {flow}.packet.header().header()... | **# flow f1 will transmit ethernet/ipv4/tcp packets** eth1,ip1,tcp1 = f1.packet.header().header().header()eth1.choice = 'ethernet'; eth1.ethernetip1.choice = 'ipv4'; ip1.ipv4tcp1.choice = 'tcp'; tcp1.tcp |

# Configuring packet headers

| **Code template** | **example** |
| --- | --- |
| **# for fixed header fields**  **{header}.{field}.value = {value}** | eth1.src.value = '00:AA:00:00:04:00'eth1.dst.value = '00:AA:00:00:00:AA' |
| **# for incrementing header fields**  **{header}.{field}.increment.start = {start}**** {header}.{field}.increment.step = {step} ****{header}.{field}.increment.count = {count}** | ip1.src.increment.start = '10.0.0.1'ip1.src.increment.step = '0.0.0.4'ip1.src.increment.count = 100 |
| **# for decrementing header fields**  **{header}.{field}.decrement.start = {start}**** {header}.{field}.decrement.step = {step} ****{header}.{field}.decrement.count = {count}** | ip1.dst.decrement.start = '10.0.0.255'ip1.dst.decrement.step = '0.0.0.1'ip1.dst.decrement.count = 100 |
| **# for value list header fields** **{header}.{field}.values = [{val1},{val2}…]** | udp1.dst\_port.values = [4000, 4044, 4060, 4074]udp2.src\_port.values = [8000, 8044, 8060] |

# Configuring captures

| **Code template** | **example** |
| --- | --- |
| cp = cfg.captures.capture(name='cp')[-1]cp.port\_names = [{port1},{port2}…] | **# configures captures on ports p1 and p2** cp = cfg.captures.capture(name='cp')[-1]cp.port\_names = ['p1', 'p2'] |

# pushing configuration

| **Code template** | **example** |
| --- | --- |
| api.set\_config({configuration}) | api.set\_config(cfg) |

# Starting captures

| **Code template** | **example** |
| --- | --- |
| cs = api.capture\_state()cs.state = cs.STARTapi.set\_capture\_state(cs) | cs = api.capture\_state()cs.state = cs.STARTapi.set\_capture\_state(cs) |

# Starting Transmit

| **Code template** | **example** |
| --- | --- |
| ts = api.transmit\_state()ts.state = ts.STARTapi.set\_transmit\_state(ts) | ts = api.transmit\_state()ts.state = ts.STARTapi.set\_transmit\_state(ts) |

# FETCHING metrics

| **Code template** | **example** |
| --- | --- |
| req = api.metrics\_request()req.port.port\_names = [{port1},{port2}…]res = api.get\_metrics(req) | **# res will contain port metrics for ports p1 and p2** req = api.metrics\_request()req.port.port\_names = ['p1', 'p2']res = api.get\_metrics(req) |

# FETCHING Captures

| **Code template** | **example** |
| --- | --- |
| req = api.capture\_request()req.port\_name = {port\_name}res = api.get\_capture(req) | **# res will contain pcap bytestream of packets captured on port p1** req = api.capture\_request()req.port\_name = 'p1'res = api.get\_capture(req) |

#

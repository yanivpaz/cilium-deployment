## Decision graph

temporary clarification before opening PR to Cilium documentation 

```mermaid
graph TD
   A{what do you need }
   A -->|Authentication| B{Need advanced Layer 7 feature ?} 
   B -->|No| D(Use light MTLS)
   B -->|Yes| E(Replace K8s kube proxy)
   E -->|Yes| M(Install Cilium service mesh)

   A -->|Encryption|H(Disalbe CNI Chaining .<br> Install Cilium CNI plugin )
   H -->  C{need FIPS?} -->|No| G(Use wireguard encryption.)
   G --> |Authentication| B
   C -->|Yes | F(Use IPSEC encryption .<br> Dont replace kube proxy)
```



## Remarks 
Disalbe CNI Chaining - remove the exising CNI ( ie - in AWS remove aws node)  
Light mtls - based on SPIFEE/SPIRE , without Envoy as sidecar .


# cilium-deployment

temp location for Cilium deployment options 

## decision graph
```mermaid
graph TD
   A{what do you need }
   A -->|Authentication| B{Need advanced Layer 7 feature ?} 
   B -->|No| D(Use light MTLS)
   B -->|Yes| E(replace K8s kube proxy)


   A -->|Encryption|H(Disalbe CNI Chaining  )
   H -->  C{need FIPS?} -->|No| G(Use wireguard encryption.)
   G --> |Authentication| B
   C -->|Yes | F(Use IPSEC encryption .<br> dont replace kube proxy)
```



## details
Disalbe CNI Chaining - remove the exising CNI ( ie - in AWS remove aws node)
Light mtls - based on SPIFEE/SPIRE , without Envoy as sidecar .

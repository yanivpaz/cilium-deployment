## Decision graph

temporary clarification before opening PR to Cilium documentation . 
the flow is based on https://isovalent.com/blog/post/2022-05-03-servicemesh-security/ .

```mermaid
graph TD
A{Need encryption ? }
A -->|No| Q( <br> Cant implement authentication) 

   
 B{Need advanced Layer 7 features ?} -->|No| D(Use Cilium MTLS,<Br> part of the Cilium CNI)
B -->|Yes| E(Replace K8s kube proxy with Cilium kube proxy)
E -->|Yes| M(Install Cilium service mesh)



A -->|Yes |H(Disalbe CNI Chaining:<br> Uninstall existing CNI plugin <br> Install Cilium CNI plugin as explained below )
H -->  C{need FIPS?} -->|No| G(Install Cilium CNI with wireguard .)
C -->|Yes | F(Install Cilium CNI with IPSEC  .<br> Dont replace k8s kube proxy)
K -->|No| X(End)

F -->|continue| T{Need authentication ?} 
T -->|Yes| D

G --> K{Need authentication ?} -->|Yes|B 
T -->|No| X(End)



```



## Remarks 
Disalbe CNI Chaining - remove the exising CNI ( ie - in AWS remove aws node)  
Light mtls - based on SPIFEE/SPIRE , without Envoy as sidecar .
Currently encryption is must for authentication - https://docs.cilium.io/en/latest/network/servicemesh/mutual-authentication/mutual-authentication/?utm_source=thenewstack&utm_medium=website&utm_content=inline-mention&utm_campaign=platform


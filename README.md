# Tigera-DPI

**Goal:** Configure Deep Packet Inspection (DPI) in clusters to get alerts on compromised resources.

Security teams need to run DPI quickly in response to unusual network traffic in clusters so they can identify potential threats. Also, it is critical to run DPI on select workloads (not all) to efficiently make use of cluster resources and minimize the impact of false positives. Calico Enterprise provides an easy way to perform DPI using Snort community rules. You can disable DPI at any time, selectively configure for namespaces and endpoints, and alerts are generated in the Alerts dashboard in Manager UI.

## Steps

1. Deploy environment

    ```bash
    # deploy Storefront Application 
    kubectl apply -f https://installer.calicocloud.io/storefront-demo.yaml
    # deploy rogue workload for testing purpose
    kubectl apply -f https://installer.calicocloud.io/rogue-demo.yaml
    ```
2. Create DeepPacketInspection resource, in this example we will enable DPI on backend pod in storefront namespace    

    ```bash
cat << EoF > DPI-storefront-backend.yaml    
apiVersion: projectcalico.org/v3
kind: DeepPacketInspection
metadata:
  name: dpi-backend
  namespace: storefront
spec:
  selector: app == "backend"
EOF
    ```

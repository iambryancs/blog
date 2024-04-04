# Add EKS ALB as origin in CloudFront with host in ingress rule

When adding an ALB as origin in CloudFront from an EKS load balancer ingress controller with host configured in ingress rule, make sure to forward the Host header in your cloudfront behavior otherwise you will always get a 502.


## Ingress
Ingress configured with host in `spec.rules.host`

```yaml
# ❯ k get ingress example-client -oyaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-client
spec:
  rules:
  - host: stage.example.com.au
    http:
      paths:
      - backend:
          service:
            name: example-client
            port:
              number: 8080
        path: /
        pathType: Prefix
```

## Origin request policy
Origin request policy with `Host` header being forwarded. This can also be done in the cache policy but we want to maximize our cache since this is a frontend app by minimizing adding any cache key such as a header.
```json
{
    "ETag": "xxx",
    "OriginRequestPolicy": {
        "Id": "xxx",
        "OriginRequestPolicyConfig": {
            "Comment": "Forward request to origin EKS alb ingress controller with host in ingress rule",
            "Name": "ForwardHostToOrigin",
            "HeadersConfig": {
                "HeaderBehavior": "whitelist",
                "Headers": {
                    "Quantity": 2,
                    "Items": [
                        "Host"
                    ]
                }
            },
            "CookiesConfig": {
                "CookieBehavior": "none"
            },
            "QueryStringsConfig": {
                "QueryStringBehavior": "none"
            }
        }
    }
}
```
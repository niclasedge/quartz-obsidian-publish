---
{}
---
# Azure Application Gateway Technical Documentation

## 1. Introduction
- Load balancer for web traffic
- Manages traffic to web apps
- Improves resiliency & distributes load

## 2. Objectives
- Identify features & use cases
- Implement gateway & select routing method
- Configure components (listeners, health probes, routing rules)

## 3. Core Functionality
- Manages requests from client apps to web apps
- Listens for incoming traffic & checks for HTTP(S) messages
- Directs traffic to resources in back-end pool

## 4. Key Benefits
- Application layer routing
- Round-robin load balancing
- Session stickiness
- Supports HTTP, HTTPS, HTTP/2, WebSocket
- Web Application Firewall (WAF)
- End-to-end encryption
- Auto-scaling

## 5. Routing Methods
1. Path-based routing: Sends requests w/ different URL paths to different back-end pools
2. Multi-site routing: Configures multiple web apps on same gateway instance
3. Redirection: Redirects traffic between listeners or to external sites
4. HTTP header rewriting: Translates URLs, query strings, modifies headers

## 6. Components
1. Front-end IP address: Receives client requests
2. Web Application Firewall (optional): Checks for threats
3. Listeners: Receive traffic & route requests
4. Routing rules: Define request analysis & direction
5. Back-end pools: Contain web servers (VMs, Scale Sets, App Service, on-premises)
6. Health probes: Determine available servers for load-balancing

## 7. Configuration Steps
1. Set up front-end IP (public/private)
2. Enable WAF (optional)
3. Configure listeners
4. Define routing rules
5. Set up back-end pools
6. Implement health probes

## 8. Best Practices
- Use path-based routing for specific URL paths
- Implement multi-site routing for multiple web apps
- Enable WAF for security
- Configure health probes for availability monitoring
- Use SSL offloading for improved performance

## 9. Additional Resources
- [Azure Application Gateway Overview](https://docs.microsoft.com/en-us/azure/application-gateway/overview)
- [Application Gateway Components](https://docs.microsoft.com/en-us/azure/application-gateway/application-gateway-components)
- [Web Application Firewall Overview](https://docs.microsoft.com/en-us/azure/web-application-firewall/ag/ag-overview)
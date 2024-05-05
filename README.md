# Curso Full Cycle 3.0 - Módulo Service Mesh com Istio

<div>
    <img alt="Criado por Alcir Junior [Caju]" src="https://img.shields.io/badge/criado%20por-Alcir Junior [Caju]-%23f08700">
    <img alt="License" src="https://img.shields.io/badge/license-MIT-%23f08700">
</div>

---

## Descrição

O Curso Full Cycle é uma formação completa para fazer com que pessoas desenvolvedoras sejam capazes de trabalhar em projetos expressivos sendo capazes de desenvolver aplicações de grande porte utilizando de boas práticas de desenvolvimento.

---

## Repositório Pai
https://github.com/alcir-junior-caju/study-full-cycle-3-0

---

## Visualizar o projeto na IDE:

Para quem quiser visualizar o projeto na IDE clique no teclado a tecla `ponto`, esse recurso do GitHub é bem bacana

---

### Service Mesh
- Service Mesh ou Malha de Serviços é uma camada extra adicionada junto ao seu cluster visando monitorar em tempo real o tráfego das aplicações, bem como elevar o nível de segurança e confiabilidade de todo o ecossistema;

### Istio
- Istio é um projeto open-source que implementa service mesh visando diminuir a complexidade no gerenciamento de aplicações distribuídas independente de qual linguagem ou tecnologia elas foram desenvolvidas;
- Ele roda em cima do Kubernetes, Apache Mesos, Consul e Nomad;
- https://istio.io;

### Por que preciso de uma Service Mesh? Istio?
- Gerenciamento de trafego;
    - Gateways (entrada e saída - Ingress e Egress);
    - Load Balancing;
    - Timeout;
    - Políticas de Retry;
    - Circuit Breaker;
    - Fault Injection;
- Observabilidade;
    - Metricas;
    - Traces distribuídos;
    - Logs;
- Segurança;
    - Man-in-the-middle;
    - mTLS;
    - AAA (Authentication, authorization e audit);

### Dinâmica && Sidecar Proxy
### Kiali - Monitoramento em tempo real

### K3D
- https://k3d.io;
- Criar um kluster: `k3d cluster create -p "8000:30000@loadbalancer" --agents 2`;

### Istioctl
- Instalar o istio com perfil default: `istioctl install`;
- Criar label: `kubectl label namespace default istio-injection=enabled`;
- Addons: https://github.com/istio/istio/tree/release-1.21/samples/addons;
- Verificar instalação: `kubectl get pods -n istio-system`;
- Abrir o `kiali`: `istioctl dashboard kiali`;

### Funcionamento Istio
- Ingress Gateway (Layer 4 a 6);
    - Ele não rotea o tráfego;
    - Ele libera as portas e trabalha com certificados;
- Virtual Service;
    - Match (Rotea os caminhos);
    - Retry (Pode confiurar as tentativas);
    - Fault Injection (Simular erros na rede);
    - Timeout;
    - Subsets (v1 e v2);
        - Destination Rule  v1;
        - Destination Rule  v2;
        - Encaminha para o workload definido nas regras;
            - Selector;
            - Tipo de Load Balancer;
            - Locality;
            - Circuit Breaker;

### Gateway (Ingress e Egress)
- Gerencia a entrada e saída do tráfego. Trabalha nos layers 4-6, garantindo o gerenciamento de portas, host, TLS. É conectado diretamente a um Virtual Service que será responsável pelo roteamento.

### Virtual Service
- Um Virtual Service permite você configurar como as requisições serão roteadas para um serviço. Ela possui uma série de regras que quando aplicadas farão com que a requisição seja direcionada ao destino correto.
    - Roteamento de trafego;
    - Subsets;
    - Fault Injection;
    - Retries;

### Destination Rules
- Você pode pensar nos Virtual Services como uma forma que você tem para rotear o tráfego para um destino, e então você usa as Destination Rules para configurar o que acontece com o tráfego quando ele chega naquele destino;

### Consistent Hash
- httpHeaderName;
- httpCookie;
- UseSourceIp;
- httpQueryParamenterName;

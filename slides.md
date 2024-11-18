---
marp: true
theme: rose-pine
paginate: true
class: lead
html: true
---

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>
<!-- _class: lead -->

# Nix en DevOps: entornos consistentes y reproducibles sin esfuerzo

## Valencia DevOps, 20/11/2024

---

# $ Whoami
🔹 Apasionado del software libre
🔹 Estudiante de doctorado en la Universidad de Castilla-La Mancha
🔹 Miembro del Summer of Nix 2024
🔹 Fediverse: [@amerinor01@mastodon.social](https://mastodon.social/@amerinor01)
🔹 Matrix: [@amerino:matrix.org](https://matrix.to/#/@amerino:matrix.org)

---

# ¿Que es Nix?
![bg vertical right 70%](imgs/file.svg)
* Gestor de Paquetes
* Sistema Operativo
* Lenguaje de Programación
* Ecosistema integral diseñado para desarrollar, implementar y gestionar software de forma reproducible.

---

# Orígenes de Nix

- Bases académicas -> Solucionar los principales problemas de la construción del software
    - Reproducibilidad:"_Build once, run everywhere_"
    - Inmutabilidad: Garantiza estados idempotentes
    - Declarativo
- [Dolstra, E. (2006). The purely functional software deployment model.](https://www.semanticscholar.org/paper/The-purely-functional-software-deployment-model-Dolstra/7c9d53d567c4db2034d8019ff11e0eb623fe2142) 

---

# Por que importa a los DevOps
- Aliniación con los principios de CI/CD
- Ya no existe el caso de "Funciona en mi maquina"
- Permite una mejores entornos compartidos entre los equipos de Dev y DevOps

---

# Reproducibilidad

- Todo en nix parte de una derivación
- Las derivaciones contienen información:
    - Dependencias
    - instrucciones de compilación / instalación
    - versiones y metadatos de la derivación
- Cada Dependencia es una propia derivación

---

# Reproductibilidad
- Cada derivación se introduce en `/nix/store/...` con un nombre único en función del resultado del binario/biblioteca
    - Multiples versiones pueden coexistir sin generar conflictos.
- Bibliotecas aisladas para cada derivación.

---


# Reproductibilidad
- __Aislamiento de red__: Nix bloquea el acceso a internet durante la construcción de paquetes para evitar dependencias no declaradas.
    - Esto garantiza que las construcciones sean reproducibles y no dependan del estado externo.


---

# Nixpkgs
![bg vertical right 90%](imgs/repo_size.svg)
- Mas de 100.000 paquetes en Nixpkgs
- Compatibilidad multiplataforma
- Permite el uso de caches para acelerar las actualizaciones

---

# NixOS
- Configuración total del sistema con expresiones Nix
- __Actualizaciones seguras y reversibles:__ Las actualizaciones son atómicas, y puedes revertir fácilmente a la configuración anterior
- Sistema Operativo declarativo e [inmutable](https://github.com/nix-community/impermanence).
- Soporte para entornos heterogéneos
    - Perminte la configuración de múltiples dispositivos con diferentes configuraciones (HPC, IoT, Escritorios)

---

# Herramientas para CI/CD
- Hydra: Construcción de pipelines de CI con Nix
- Cachix: Herramienta de caches para derivaciones Nix

---

# Estandarización del entorno de trabajo con Nix
- DevBox: Configura rápidamente espacios de trabajo aislados para pruebas y desarrollo.
- DevShell: Crea entornos de desarrollo bajo demanda, adaptados a las necesidades del proyecto.
- Flakes: Un estándar moderno para la reproducibilidad y la gestión estructurada de proyectos
    - Incluido en Nix.
---

# Casos de Uso Avanzados
- [NixOps](https://github.com/NixOS/nixops): Automatización de despliegues
- Construcción y ejecución de contenedores con [dockerTools](https://nix.dev/tutorials/nixos/building-and-running-docker-images.html)
- [Colmena](https://github.com/zhaofengli/colmena): Orquestación ligera
- [Home Manager](https://github.com/nix-community/home-manager): Entornos de usuario declarativos
- Integraciones con herramientas como [Terraform](https://github.com/stackbuilders/nixpkgs-terraform/), Helm(con [Kubenix](https://kubenix.org/modules/helm/) ), etc.

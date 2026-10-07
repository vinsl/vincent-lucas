# Vincent Lucas

**Junior DevOps & Cloud Engineer** · Linux · AWS · Terraform / OpenTofu · Puppet / OpenVox · Ansible · Kubernetes · CI/CD · Python

Dual master's degrees in Computer Science (Mines Saint-Étienne, ISMIN) and Software Engineering (University of Technology Sydney). Based in Aix-en-Provence, France.

I started on small systems I could hold in my hands: a robot driven by a Raspberry Pi over SSH, then a web tool installed on a school's Linux server. The projects below apply the same work to fleets of machines, described as code. Each one was deployed for real, validated, then destroyed to keep costs down. The READMEs keep the evidence and what broke along the way.

## Infrastructure projects

Self-training projects, built to learn each tool by running it.

### [HTCondor Batch Farm as Code](https://github.com/vinsl/HTCondor-Batch-Farm)

<a href="https://vinsl.github.io/HTCondor-Batch-Farm/docs/lab/visuals/">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github.com/vinsl/HTCondor-Batch-Farm/raw/main/docs/lab/visuals/hero-dark.png">
    <img src="https://github.com/vinsl/HTCondor-Batch-Farm/raw/main/docs/lab/visuals/hero-light.png" width="100%" alt="3D view of the lab: a central manager and two workers on AWS, with the OpenVox and HTCondor flows between them.">
  </picture>
</a>

A batch-computing pool on AWS, built and configured entirely from code. OpenTofu creates three AlmaLinux 9 machines, Ansible gives each one the minimum needed to join, and an OpenVox (open source Puppet) server configures them and reverts manual changes. New nodes are admitted by policy-based certificate signing, and their role is carried in the signed certificate. A Python health check makes a faulty worker refuse jobs until Puppet has repaired it.

A fourth node added in code joined the pool and ran jobs in 4 min 18 s with no manual step. The whole lab is rebuilt from nothing in about 15 minutes, and every pull request runs puppet-lint, rspec-puppet, ansible-lint, tofu validate, Checkov, Gitleaks, Ruff and Pytest.

`OpenTofu` `Ansible` `OpenVox / Puppet` `Hiera` `HTCondor` `AlmaLinux` `GitHub Actions` · [Interactive 3D model of the lab](https://vinsl.github.io/HTCondor-Batch-Farm/docs/lab/visuals/)

### [Highly Available Support Desk: AWS ECS Fargate & Kubernetes](https://github.com/vinsl/support-desk-ecs-kubernetes)

A Flask support-ticket application with a MySQL database, deployed two ways. On AWS with modular Terraform: two ECS Fargate tasks behind an Application Load Balancer, RDS MySQL in private subnets, logs in CloudWatch. On Kubernetes as a single Helm chart: Deployment with readiness and liveness probes, Ingress, MySQL StatefulSet, and a migration Job run as a Helm hook.

On a multi-node kind cluster I validated self-healing, zero-downtime rolling updates, Helm rollback and data persistence after deleting every application Pod.

`Terraform` `ECS Fargate` `ALB` `RDS` `Docker` `Kubernetes` `Helm` `ingress-nginx`

### [Secure CI/CD Platform to AWS](https://github.com/vinsl/aws-cicd-platform)

A GitHub Actions pipeline that delivers a containerised Flask app to ECS Fargate. Each pull request runs Pytest, Ruff, a Docker build, Terraform validation, Checkov, Gitleaks and Trivy, without any AWS credentials. On merge to main, the pipeline authenticates to AWS through OIDC, pushes a SHA-tagged image to ECR, registers a new task definition and runs a rolling deployment checked by a smoke test on the load balancer.

Terraform state is stored in an encrypted, versioned S3 bucket with native locking, and the rollback procedure is documented.

`GitHub Actions` `OIDC` `Terraform` `ECR` `ECS Fargate` `Trivy` `Checkov` `Gitleaks`

### [Serverless Task API on AWS](https://github.com/vinsl/serverless-task-api-aws)

A CRUD REST API in Python on API Gateway, Lambda and DynamoDB, provisioned entirely with Terraform. The Lambda validates requests, generates IDs and timestamps server-side, and uses conditional DynamoDB writes to return proper 404s. It runs with a least-privilege IAM role and is covered by 11 Pytest unit tests.

`API Gateway` `Lambda` `DynamoDB` `IAM` `CloudWatch` `Terraform` `Pytest`

## Work delivered for others

### [Class Allocation Tool](https://github.com/vinsl/class-allocation-tool) · freelance, 2026

A Flask tool that turns a cohort spreadsheet into balanced, constraint-aware class assignments. I deployed and maintained it on the internal Linux server of a 1,300-student international school in Sydney, where it satisfies 98% of the allocation criteria and saves around 50 teacher hours per year. The production code is proprietary; the repository holds the documentation, anonymised examples and the [product page](https://vinsl.github.io/class-allocation-tool/).

`Python` `Flask` `Linux` `Excel workflows`

### [Autonomous Tennis Ball Collector Robot](https://github.com/vinsl/autonomous-ball-collector-robot) · robotics internship, 2025

Selected parts of a 12-week internship in a robotics start-up. I set up a Raspberry Pi 5 as a headless Linux control unit administered over SSH, wrote the Flask server that translates HTTP commands into a serial G-Code-style protocol for the ESP32, and trained a ball-detection model reaching a mAP of about 0.93 at more than 1 FPS on the Pi.

`Linux` `Raspberry Pi 5` `Flask` `ESP32` `Serial` `Computer vision`

### Research Engineer · University of Technology Sydney, 2025–2026

Compared Linear Regression, Random Forest and Support Vector Regression for coal-mine gas warning systems across 39 performance metrics, in Python with scikit-learn. I coordinated a six-person research team and wrote the paper, now under review.

## Toolbox

| | |
|---|---|
| **Systems & batch** | Linux (RHEL family, systemd, firewalld), SSH, Bash, HTCondor |
| **Configuration & IaC** | Terraform / OpenTofu, OpenVox / Puppet (roles and profiles, Hiera, EPP), Ansible |
| **Containers & cloud** | Docker, Kubernetes (Helm, Ingress, probes), AWS (EC2, VPC, ECS Fargate, ALB, RDS, Lambda, API Gateway, DynamoDB, IAM, CloudWatch) |
| **CI/CD & quality** | GitHub Actions, Pytest, Ruff, rspec-puppet, ansible-lint, Checkov, Gitleaks, Trivy |
| **Code** | Python, C, C++, Git |

## Currently

- Looking for a junior DevOps / Cloud Engineer role in Switzerland, available from 1 December 2026.
- Preparing the AWS Certified Solutions Architect – Associate exam (SAA-C03), planned for October 2026.

## Contact

- Email: [vincentselucas@gmail.com](mailto:vincentselucas@gmail.com)
- LinkedIn: [linkedin.com/in/vincent-lucas-483b29295](https://www.linkedin.com/in/vincent-lucas-483b29295/)
- Languages: French (native), English (C1), Italian (B2), German (A1, learning)

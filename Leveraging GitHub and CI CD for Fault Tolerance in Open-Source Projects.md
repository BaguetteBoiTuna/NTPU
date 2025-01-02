# Leveraging GitHub and CI/CD for Fault Tolerance in Open-Source Projects

- **Authors**:
  - Dante Guillemain (711382799)
  - Jules Trolle (711333199)

## Abstract

This report explores how open-source projects achieve fault tolerance while managing contributions from large, distributed teams. By leveraging tools like Git, GitHub workflows, and CI/CD pipelines, these projects ensure software reliability, scalability, and efficiency. A case study on the JavaScript runtime Bun illustrates practical fault-tolerant practices, including modular pipelines, automated testing, and parallel builds. The findings highlight the importance of robust automation, collaborative workflows, and effective monitoring in maintaining fault-tolerant systems. Insights from this study can guide future improvements and inspire broader adoption of these practices across open-source projects.

## Introduction

Fault tolerance is a critical concept in software development, ensuring that systems continue to operate effectively even in the presence of faults or failures. For open-source projects, fault tolerance becomes even more essential due to the decentralized and collaborative nature of development, involving contributors from diverse backgrounds and expertise levels.

Open-source projects, such as Linux, TensorFlow, and Homebrew, rely heavily on tools like Git and GitHub to manage contributions, maintain consistency, and ensure reliability. These tools, combined with Continuous Integration/Continuous Deployment (CI/CD) pipelines, play a vital role in mitigating risks, automating error detection, and streamlining collaboration.

This report focuses on how open-source projects achieve fault tolerance by leveraging these tools and practices. It aims to provide insights into the challenges faced, the solutions implemented, and the lessons learned, using the JavaScript runtime Bun as a detailed case study.

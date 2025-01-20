<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a id="readme-top"></a>


## pladground

An active directory playground/lab for penetration testing and learning.


This lab is made of five virtual machines:
- **Domain Controller** running Windows Server 2019
- **Member Server** running IIS and MSSQL
- **Windows Workstation** running on Windows 10
- **Linux Server inside the domain** running Ubuntu 20.04 LTS
- **Linux Server outside the domain** running Ubuntu 20.04 LTS

<!-- GETTING STARTED -->
## Getting Started

To start the lab on your machines the following prerequisites exist.

### Prerequisites

In order to run this setup you need `vagrant` and `ansible`.
Depending on your host machine, you can install them via:

* `vagrant` on debian-based systems. Otherwise refer to [vagrant's own page](https://developer.hashicorp.com/vagrant/downloads).
  ```sh
  wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
  echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
  sudo apt update && sudo apt install vagrant
  ```
* `ansible`, also refer to [their site](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#pipx-install)
  ```sh
  $ pipx install --include-deps ansible
  ```

### Installation

To download the lab and install it, follow the following steps:

1. Clone the repo
   ```sh
   git clone https://github.com/Benzammour/PlADground
   ```
3. Download and Run Base VMs
   ```sh
   vagrant up
   ```
4. Run `ansible` playbook
   ```sh
   ansible-playbook -vv -i hosts labsetup.yml
   ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage

To download and use lab, you have to clone the repo and run both vagrant and ansible.
tl;dr: Follow the following steps:

1. Clone the repo
   ```sh
   git clone https://github.com/Benzammour/PlADground
   ```
3. Download and Run Base VMs
   ```sh
   vagrant up
   ```
4. Run `ansible` playbook
   ```sh
   ansible-playbook -vv -i hosts labsetup.yml
   ```

To run different portions of the lab or for debugging purposes, run the playbooks independently:
```sh
ansible-playbook -i hosts domain_controller.yml
ansible-playbook -i hosts member_server.yml
ansible-playbook -i hosts win_workstation.yml
ansible-playbook -i hosts linux_srv_domain.yml
ansible-playbook -i hosts linux_srv_no_domain.yml
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- Issues and Features -->
## Issues and Features

See the [open issues](https://github.com/benzammour/pladground/issues) for a full list of proposed features (and known issues).

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- CONTACT -->
## Contact

Your Name - [@benzammour](https://infosec.exchange/@benzammour)

Project Link: [https://github.com/benzammour/pladground](https://github.com/benzammour/pladground)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

* [alebov](https://github.com/alebov) for original [AD-lab repo](https://github.com/alebov/AD-lab)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

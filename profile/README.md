<a name="readme-top"></a>

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]
[![Discord][discord-shield]][discord-url]
[![Modrinth][modrinth-shield]][modrinth-url]

<br />
<div align="center">
  <a href="https://github.com/fstats/fstats">
    <img src="https://fstats.dev/icon.png" alt="Logo" width="80" height="80">
  </a>

<h3 align="center">fStats</h3>

  <p align="center">
    Fabric metric system for developers
    <br />
    <a href="https://discord.gg/pbwnMwnUD6">Support</a>
    ·
    <a href="https://github.com/fstats/fstats-api/issues">Report Bug</a>
    ·
    <a href="https://github.com/fstats/fstats-api/issues">Request Feature</a>
  </p>
</div>

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-the-project">About The Project</a></li>
    <li>
        <a href="#usage">Usage</a>
        <ul>
            <li><a href="#for-users">For users</a></li>
            <li><a href="#for-developers">For developers</a></li>
        </ul>
    </li>
    <li><a href="#structure">Structure</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li>
      <a href="#contributing">Contributing</a>
      <ul>
        <li><a href="#localization">Localization</a></li>
      </ul>
    </li>
    <li><a href="#license">License</a></li>
  </ol>
</details>

## About The Project

![Project Page Preview](https://cdn.modrinth.com/data/DkOr2M32/images/70d32b52147ef1d0431ffc31bb2241a743eaeb91.png)

fStats is a 3rd-party metric collection library. The Main idea of is help developers to recognize their actual community based
on charts

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Usage

### For user

Mod have config that allows to turn off a metric collection and hiding location

> ../config/fstats-api/config.json
<details>
<summary>v2</summary>

```json5
{
  "version": 2,  // Config version
  "mode": "ALL", // Data collecting mode [ ALL | WITHOUT_LOCATION | NOTHING ]
  "messages": {
    "infos": true,
    "warnings": true,
    "errors": true
  }
}
```

</details>

<details>
<summary>v1</summary>

```json5
{
    "enabled": true,      // Enable/Disable collection from our server
    "hideLocation": false // Mod not collect your IP, only country name 
}
```

</details>

### For developers

Up-to-date guide can be found here: https://fstats.dev/getting-started

Also, recommend adding the badge to your project description to notify users that you collect information. 

*Resize the badge to any size that you want*
![Badge](https://cdn.modrinth.com/data/DkOr2M32/images/597e8bc81f48ad606ae5624f566994dde65ac409.png)

fStats also has [Image Generator](https://img.fstats.dev/) for webpages or markdown including and [UI editor](https://fstats.github.io/fstats-image-generator-editor/) for it

![fStats Chart](https://img.fstats.dev/v2/timeline/1?theme=light&format=svg&mode=week&width=800&height=300&client_color=alizarin&server_color=peter-river)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Structure

```mermaid
%%{
  init: {
    'theme': 'dark',
    'themeVariables': {
      'primaryColor': '#20242d',
      'primaryTextColor': '#ffffff',
      'primaryBorderColor': '#58a6ff',
      'lineColor': '#7d8590',
      'secondaryColor': '#20242d',
      'tertiaryColor': '#20242d'
    }
  }
}%%
graph TD
    subgraph " "
        direction LR
        subgraph "User Related"
            Frontend("Frontend")
            Minecraft("Minecraft Client")
        end

        subgraph "Core Infrastructure"
            Backend("Backend")
        end

        subgraph "Data & Caching"
            direction TB
            Kafka("Kafka")
            ClickHouse("ClickHouse")
            PostgreSQL("PostgreSQL")
            Dragonfly("Dragonfly (Redis cache)")
            ImageGenerator("Image Generator")
        end
    end


    %% Connections
    Frontend -- "REST API" <--> Backend;
    Minecraft -- "Metric POST" --> Backend;

    Backend -- "Metric POST" --> Kafka;
    Backend -- "Primary Database" <--> PostgreSQL;
    Backend -- "Metric REST" --> ClickHouse;

    Kafka -- "Kafka Engine" --> ClickHouse;

    Backend -- "REST" --> ImageGenerator;
    ImageGenerator -- "Cache" <--> Dragonfly;

    %% Styling
    style Frontend fill:#161b22,stroke:#30363d,stroke-width:2px;
    style Minecraft fill:#161b22,stroke:#30363d,stroke-width:2px;
    style Backend fill:#161b22,stroke:#58a6ff,stroke-width:2px;

    classDef data fill:#161b22,stroke:#30363d,stroke-width:2px;
    class Kafka,ClickHouse,PostgreSQL,Dragonfly,ImageGenerator data;
```

See the [open issues](https://github.com/fstats/fstats-api/issues) for a full list of proposed features (and known
issues).

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Roadmap
You can find the roadmap and related here: https://github.com/orgs/fStats/projects/1

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any
contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also
simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Localization
fStats has many modules and all of them have different ways to localize, so check the table below to find the right guide.

|Module|Guide|
|--|--|
|Frontend|[Link](https://github.com/fStats/fstats-frontend?tab=readme-ov-file#localization)|
|Backend|Unsupported|
|Image Generator|Unsupported|
|Image Generator Editor|[Link](https://github.com/fStats/fstats-image-generator-editor?tab=readme-ov-file#localization)|
|Minecraft API|[Link](https://github.com/fStats/fstats-api?tab=readme-ov-file#localization)|

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

[contributors-shield]: https://img.shields.io/github/contributors/fstats/fstats-api.svg?style=for-the-badge

[contributors-url]: https://github.com/fstats/fstats-api/graphs/contributors

[forks-shield]: https://img.shields.io/github/forks/fstats/fstats-api.svg?style=for-the-badge

[forks-url]: https://github.com/fstats/fstats-api/network/members

[stars-shield]: https://img.shields.io/github/stars/fstats/fstats-api.svg?style=for-the-badge

[stars-url]: https://github.com/fstats/fstats-api/stargazers

[issues-shield]: https://img.shields.io/github/issues/fstats/fstats-api.svg?style=for-the-badge

[issues-url]: https://github.com/fstats/fstats-api/issues

[license-shield]: https://img.shields.io/github/license/fstats/fstats-api.svg?style=for-the-badge

[license-url]: https://github.com/fstats/fstats-api/blob/master/LICENSE.txt

[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555

[linkedin-url]: https://linkedin.com/in/kit-lehto

[discord-shield]: https://img.shields.io/discord/1032138561618726952?logo=discord&logoColor=white&style=for-the-badge&label=Discord

[discord-url]: https://discord.gg/pbwnMwnUD6

[modrinth-shield]: https://img.shields.io/modrinth/v/fstats-api?label=Modrinth&style=for-the-badge

[modrinth-url]: https://modrinth.com/mod/fstats

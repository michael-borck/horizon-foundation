# Horizon Foundation

A powerful static site generator and HTML template renderer built with the Jinja templating engine. Horizon Foundation enables developers to create dynamic, scalable websites using layouts, includes, and sophisticated content generation without requiring a complex backend infrastructure.

## Overview

Horizon Foundation streamlines the process of building static websites by leveraging Jinja's templating capabilities. Whether you're creating documentation sites, organizational portals, or multi-page websites, this tool provides a flexible and efficient solution for managing templates, layouts, and dynamic content generation.

## Features

- **Jinja Template Support**: Full support for Jinja2 templating engine with advanced features
- **Layout Management**: Create reusable base layouts and extend them across multiple pages
- **Template Includes**: Modular content organization with include directives
- **Dynamic Content Generation**: Render static HTML from dynamic data sources
- **Static Asset Pipeline**: Integrated CSS and JavaScript asset management
- **Flexible Configuration**: YAML-based configuration for project setup
- **GitHub Pages Integration**: Built-in GitHub Actions workflow for automated deployment

## Installation

### Prerequisites

- Python 3.7 or higher
- pip (Python package installer)

### Setup

1. Clone the repository:

```bash
git clone https://github.com/michael-borck/horizon-foundation.git
cd horizon-foundation
```

2. Install required dependencies:

```bash
pip install -r requirements.txt
```

3. Verify the installation:

```bash
python -m horizon --version
```

## Usage

### Basic Configuration

Create a `brief.yaml` configuration file in your project root:

```yaml
site:
  title: "My Site"
  description: "Site description"
  output_dir: "dist"
  
content:
  source_dir: "content"
  
templates:
  dir: "templates"
```

### Project Structure

Organize your project with the following structure:

```
project-root/
├── brief.yaml                 # Site configuration
├── templates/                 # Jinja template files
│   ├── base.html             # Base layout
│   ├── layouts/              # Layout templates
│   └── includes/             # Reusable components
├── content/                  # Content source files
│   ├── docs/                 # Documentation
│   ├── employees/            # Employee information
│   └── jobs/                 # Job listings
├── assets/                   # Static assets
│   ├── css/
│   └── js/
└── dist/                     # Generated output directory
```

### Creating Templates

Base layout (`templates/base.html`):

```jinja
<!DOCTYPE html>
<html>
<head>
    <title>{{ page_title }} - {{ site_title }}</title>
    {% include 'includes/meta.html' %}
</head>
<body>
    {% include 'includes/header.html' %}
    <main>
        {% block content %}{% endblock %}
    </main>
    {% include 'includes/footer.html' %}
</body>
</html>
```

Child template (`templates/page.html`):

```jinja
{% extends "base.html" %}

{% block content %}
<article>
    <h1>{{ title }}</h1>
    {{ content }}
</article>
{% endblock %}
```

### Building Your Site

Generate the static site:

```bash
python -m horizon build
```

This command will:
- Read all configuration from `brief.yaml`
- Process Jinja templates with your content
- Copy static assets to output directory
- Generate HTML files in the `dist/` directory

### Serving Locally

Preview your site locally:

```bash
python -m horizon serve
```

The site will be available at `http://localhost:8000`

## Content Organization

### Markdown Integration

Place Markdown files in the `content/` directory. Horizon Foundation automatically processes these with YAML frontmatter:

```markdown
---
title: "Page Title"
layout: "page"
author: "Author Name"
---

# Content starts here

Your markdown content...
```

### Directory Structure Examples

Policy documents:
```
content/docs/policy/
├── donor-privacy-and-ethical-fundraising-policy.md
└── safeguarding-and-child-protection-policy.md
```

Support resources:
```
content/docs/support/
├── grant-writing-guide.md
├── program-impact-report-template.md
└── volunteer-handbook.md
```

Team information:
```
content/employees/
├── amara-osei.md
└── amara-osei-prompt.txt
```

## Configuration

### brief.yaml Options

```yaml
site:
  title: string              # Site name
  description: string        # Site description
  url: string               # Site base URL
  output_dir: string        # Output directory (default: dist)
  
content:
  source_dir: string        # Content source directory
  
templates:
  dir: string              # Templates directory
  
assets:
  dir: string              # Static assets directory
```

## Deployment

### GitHub Pages

Horizon Foundation includes an automated GitHub Actions workflow (`.github/workflows/pages.yml`) that:
- Builds your site on every push
- Deploys to GitHub Pages automatically
- Requires minimal configuration

Enable GitHub Pages in your repository settings and push to deploy.

## Advanced Features

### Template Filters

Extend Jinja with custom filters for enhanced functionality:

```jinja
{{ content | markdown }}
{{ date_string | format_date('%B %d, %Y') }}
{{ text | truncate(50) }}
```

### Global Context

Pass global variables to all templates via configuration:

```yaml
globals:
  organization: "Horizon Foundation"
  current_year: 2024
```

Access in templates:

```jinja
<footer>
  <p>&copy; {{ current_year }} {{ organization }}</p>
</footer>
```

### Custom Plugins

Extend functionality with custom Python modules in the `plugins/` directory for specialized content processing.

## Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit your changes (`git commit -am 'Add improvement'`)
4. Push to the branch (`git push origin feature/improvement`)
5. Submit a Pull Request

## Documentation

For detailed documentation, guides, and examples, see the `content/docs/` directory which includes:

- Policy documentation
- Support guides and templates
- Grant writing resources
- Volunteer handbook

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For issues, questions, or suggestions, please open an issue on the GitHub repository.

## Author

Created and maintained by [michael-borck](https://github.com/michael-borck)
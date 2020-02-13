# Magento 2 Certified Associate Developer Exam Notes

## 📝 Table of Contents
- [Exam Structure](#exam-structure)
- [Exam Content](#exam-content)
  - [Magento Architecture & Customisation Techniques](#10-magento-architecture--customisation-techniques)
  - [Request Flow Processing](#20-request-flow-processing)
  - [Customising Magento UI](#30-customising-the-magento-ui)
  - [Working with Magento Databases](#40-working-with-databases-in-magento)
  - [Developing with Adminhtml](#50-developing-with-adminhtml)
  - [Customising Magento Business Logic](#60-customising-magento-business-logic)
- [References](#references) 

## ⛏️ Exam Structure
### Associate Developer
|       |       |
| :---: | :---: |
| Magento Version | 2.3.x |
| Magento Theme | Luma |
| Number of Questions | 60 |
| Time Limit | 90 Minutes |
| Passing Grade | 68% |

<br>

## ✍️ Exam Content
### 1. Magento Architecture & Customisation Techniques

This section accounts for **33%** of the test.

#### 1.1. Describe the Magento module-based architecture

##### Describe module architecture.

> What are the significant steps to add a new module?

You need to create the following files:
- `registration.php`
- `etc/module.xml`

##### `registration.php`
This file is included by the Composer autoloader and is added to the static list of components in `Magento\Framework\Component\ComponentRegistrar`. Example:

```PHP
<?php
use \Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,        // type
    'YourCompany_YourModule',          // componentName
    __DIR__                            // path
);
```

Once Magento has found this file, it will then look to find `etc/module.xml`.

##### `module.xml`
A component declares itself (that is, defines its name and existence) in the `module.xml` file located in the module's `etc/` directory.
This file specifies the loading sequence for the module and its setup version (if not using Declarative Schema).

The sequence tells Magento which order to load modules in. This is done in `Magento\Framework\Module\ModuleList\Loader.php` and only occurs when the module is installed.
This sequence is useful for events, plugins, preferences, and layouts.
- **NB:** If your module modifies the layout of another and your module is loaded first, the other module will overwrite your modifications.

Example:
```XML
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="YourCompany_YourModule">
        <sequence>
            <module name="TheirCompany_TheirModule" />
            <module name="AnotherCompany_AnotherModule" />
        </sequence>
    </module>
</config>
```

---
> What are the different Composer package types?

| Name  | Package Type | Description |
| :---: | :----------: | :---------- |
| Metapackage | metapackage | Technically, a Composer package type, not a Magento component type. A metapackage consists of only a `composer.json` file that specifies a list of components and their dependencies. For example, both Magento Open Source and Magento Commerce are metapackages. |
| Module | magento2-module | Code that modifies Magento application behavior. You can upload a single module to the Magento Marketplace or your module can be dependent on some parent package. |
| Theme | magento2-theme | Code that modifies the look and feel of the storefront or Magento Admin. |
| Language Package | magento2-language | Translations for the storefront or Admin. |

---
> When would you place a module in the app/code folder versus another location?

In most cases, the modules that you develop go into `app/code/CompanyName`. This is the namespace used for development.
Modules are placed in the folder directly below. With Magento’s dependency on Composer, you can theoretically import modules from almost any location in a project.

---
#### 1.2. Describe the Magento Directory Structure

##### Describe the Magento directory structure.

> What are the naming conventions, and how are namespaces established?


---
> How can you identify the files responsible for some functionality?

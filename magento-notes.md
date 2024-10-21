# Magento Cheat Sheet

## 1. Magento Directory Structure

- **app/**: Contains code, design, and configuration files.
  - **code/**: Custom modules.
  - **design/**: Layout and template files.
  - **etc/**: Configuration files.
  - **i18n/**: Translation files.
- **pub/**: Web-accessible content (CSS, JS, images).
- **var/**: Generated files, cache, and logs.
- **vendor/**: Composer-installed dependencies.
- **lib/**: Core Magento library files.
- **bin/**: Magento CLI command-line tool.

## 2. Magento 2 CLI Commands

- **General Commands**:
  - Clear Cache:
    ```bash
    bin/magento cache:clean
    ```
  - Flush Cache:
    ```bash
    bin/magento cache:flush
    ```
  - Reindex:
    ```bash
    bin/magento indexer:reindex
    ```
  - Upgrade Database:
    ```bash
    bin/magento setup:upgrade
    ```
  - Static Files Deployment:
    ```bash
    bin/magento setup:static-content:deploy
    ```
  - Enable Maintenance Mode:
    ```bash
    bin/magento maintenance:enable
    ```
  - Disable Maintenance Mode:
    ```bash
    bin/magento maintenance:disable
    ```
  - Check Maintenance Mode Status:
    ```bash
    bin/magento maintenance:status
    ```

## 3. Magento 2 Configuration Files

- **env.php**: Stores environment configuration.
- **config.php**: Stores module enable/disable statuses.

## 4. Module Development

- **Create a Module**:
  - Create `app/code/Vendor/ModuleName/registration.php`:
    ```php
    \Magento\Framework\Component\ComponentRegistrar::register(
        \Magento\Framework\Component\ComponentRegistrar::MODULE,
        'Vendor_ModuleName',
        __DIR__
    );
    ```
  - Add `app/code/Vendor/ModuleName/etc/module.xml`:
    ```xml
    <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
        <module name="Vendor_ModuleName" setup_version="1.0.0"/>
    </config>
    ```

## 5. Magento 2 Layout XML Files

- **Page Layout** (app/design/frontend/Vendor/Theme/Magento_Theme/layout/default.xml):

  ```xml
  <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
      <body>
          <referenceContainer name="content">
              <block class="Vendor\Module\Block\Custom" name="custom.block" template="Vendor_Module::custom.phtml"/>
          </referenceContainer>
      </body>
  </page>
  ```

- **Block Definition in Layout**:
  ```xml
  <block class="Magento\Catalog\Block\Product\View" name="custom_product_block" template="Vendor_Module::custom_product.phtml"/>
  ```

## 6. Creating Blocks

- **Block Class** (app/code/Vendor/Module/Block/Custom.php):
  ```php
  namespace Vendor\Module\Block;

  class Custom extends \Magento\Framework\View\Element\Template
  {
      public function getCustomData()
      {
          return 'Custom Data';
      }
  }
  ```
- **Custom Template** (app/code/Vendor/Module/view/frontend/templates/custom.phtml):
  ```php
  <h2><?php echo $block->getCustomData(); ?></h2>
  ```

## 7. Observer Creation

- **events.xml** (app/code/Vendor/Module/etc/frontend/events.xml):

  ```xml
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Event/etc/events.xsd">
      <event name="controller_action_predispatch">
          <observer name="custom_observer" instance="Vendor\Module\Observer\CustomObserver"/>
      </event>
  </config>
  ```

- **Observer Class** (app/code/Vendor/Module/Observer/CustomObserver.php):
  ```php
  namespace Vendor\Module\Observer;

  use Magento\Framework\Event\Observer;
  use Magento\Framework\Event\ObserverInterface;

  class CustomObserver implements ObserverInterface
  {
      public function execute(Observer $observer)
      {
          // Add custom logic here
      }
  }
  ```

## 8. Magento 2 Database Interaction

- **Fetching Data Using Model**:

  ```php
  $product = $this->_objectManager->create('Magento\Catalog\Model\Product')->load($productId);
  ```

- **Repository Pattern (Recommended)**:
  ```php
  $productRepository = $this->_objectManager->get('\Magento\Catalog\Api\ProductRepositoryInterface');
  $product = $productRepository->getById($productId);
  ```

## 9. Magento 2 Cache Types

- Block HTML output:
  ```bash
  bin/magento cache:clean block_html
  ```
- Configuration:
  ```bash
  bin/magento cache:clean config
  ```
- Full Page Cache:
  ```bash
  bin/magento cache:clean full_page
  ```

## 10. Common Database Tables

- **catalog_product_entity**: Stores product details.
- **sales_order**: Stores sales order information.
- **customer_entity**: Stores customer information.
- **quote**: Stores cart information before it's converted to an order.

## 11. Theme Development

- **Create a Theme Directory**:
  ```
  app/design/frontend/Vendor/theme_name/
  ```
- **Registration**:
  ```php
  // app/design/frontend/Vendor/theme_name/registration.php
  \Magento\Framework\Component\ComponentRegistrar::register(
      \Magento\Framework\Component\ComponentRegistrar::THEME,
      'frontend/Vendor/theme_name',
      __DIR__
  );
  ```
- **Theme Layout**:
  ```
  app/design/frontend/Vendor/theme_name/Magento_Theme/layout/default.xml
  ```

## 12. Magento User Roles and Permissions

- Navigate to **System** > **Permissions** > **User Roles**.
- Create or edit roles and assign permissions for admin users.

## 13. Debugging Magento

- Enable Developer Mode:
  ```bash
  bin/magento deploy:mode:set developer
  ```
- Enable Error Reporting:
  ```php
  ini_set('display_errors', 1);
  ini_set('display_startup_errors', 1);
  error_reporting(E_ALL);
  ```

## 14. Useful SQL Queries

- **List All Products**:
  ```sql
  SELECT * FROM catalog_product_entity;
  ```
- **Find Orders by Customer**:
  ```sql
  SELECT * FROM sales_order WHERE customer_email = 'customer@example.com';
  ```

## 15. Magento Logs

- **System Log**:  
  `var/log/system.log`
- **Exception Log**:  
  `var/log/exception.log`

## 16. Customizing Email Templates

- Path:  
  `app/code/Vendor/Module/view/frontend/email/custom_email_template.html`

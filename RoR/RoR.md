### Add page (route)
- Create route (`config/routes.rb`):
  `get 'welcome', to: 'pages#welcome'`
- Create controller (`app/controllers`):
  - Add page to `pages_controller`:
  - ```
    def main

    end
    ```
- Create page in `app/views/pages`
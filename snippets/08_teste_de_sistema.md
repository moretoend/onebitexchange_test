# Teste de Sistema

Nesta aula faremos o teste do fluxo do usuário, conhecido como teste de sistema



**1 – Crie uma pasta em `spec/system`, dentro dela crie um arquivo chamado `exchange_index_system_spec.rb`**

```shell
mkdir spec/system
touch spec/system/exchange_index_system_spec.rb
```



**2- Dentro desse arquivo coloque:**

```ruby
require 'rails_helper'

RSpec.describe "Exchange Currency Process", :type => :system, js: true do
  it "exchange value" do
    visit '/'
    within("#exchange_form") do
      select('EUR', from: 'source_currency')
      select('USD', from: 'target_currency')
      fill_in 'amount', with: rand(1..9999)
    end
    click_button 'CONVERTER'

    # save_and_open_page
    expect(page).to have_content("value")
  end
end
```



**3- Rode o teste:**

```shell
docker-compose run --rm app bundle exec rspec spec/system/exchange_index_system_spec.rb
```



**4 – Coloque no rails_helper.rb (dentro das configurações):**

```ruby
config.before(:each, type: :system) do
  driven_by :rack_test
end
```



**BRANCH:** *system_spec*
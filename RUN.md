# Project structure
- Rockelivery -> Facade

# test new schema/model
user_params = %{
    age: 27, 
    address: "Rua cecílio batista marques", 
    cep: "123",
    cpf: "123",
    email: "phablovilasboas25@gmail.com",
    password_hash: "123",
    name: "Phablo Vilas Boas"
};

alias Rockelivery.User
User.changeset(user_params)

# Testing invalid fields
invalid_params = %{
    address: "Rua cecílio batista marques", 
    cep: "123",
    cpf: "123",
    email: "phablovilasboas25@gmail.com",
    password_hash: "123",
    name: "Phablo Vilas Boas"
};

alias Rockelivery.User
User.changeset(invalid_params)

# All fields valid:

user_params = %{
    age: 27, 
    address: "Rua cecílio batista marques", 
    cep: "44250000",
    cpf: "03960591551",
    email: "phablovilasboas25@gmail.com",
    password_hash: "!123Mudar",
    name: "Phablo Vilas Boas"
}

# ADD pbkdf2_elixir to hash passwords
- using
- Pbkdf2.add_hash("123456")

# test with password virtual:
user_params = %{
    age: 27, 
    address: "Rua cecílio batista marques", 
    cep: "44250000",
    cpf: "03960591551",
    email: "phablovilasboas25@gmail.com",
    password: "!123Mudar",
    name: "Phablo Vilas Boas"
}
alias Rockelivery.User
User.changeset(user_params)


# testing Repo
alias Rockelivery.User
alias Rockelivery.Repo

user_params = %{
    age: 27, 
    address: "Rua cecílio batista marques", 
    cep: "44250000",
    cpf: "03960591551",
    email: "phablovilasboas25@gmail.com",
    password: "!123Mudar",
    name: "Phablo Vilas Boas"
}

user_params 
    |> User.changeset() 
    |> Repo.insert()


# Testing User.by_id
alias Rockelivery.{Repo, User}
alias Rockelivery.Users.Get

Repo.all(User)   -> Get one Id
Get.by_id("555") -> Error
Get.by_id("aa283f2b-6fd3-4204-9903-338658f46d36") -> Success
Get.by_id("aa283f2b-6fd3-4204-9903-338658f46d38") -> Not Found

versão com with
Get.by_idv2("aa283f2b-6fd3-4204-9903-338658f46d36") -> Sucess
Get.by_idv2("555") -> Id inválido
Get.by_idv2("aa283f2b-6fd3-4204-9903-338658f46d38") -> Not Found

# Test Get User
curl --location --request GET \
'http://localhost:4000/api/users/283f2b-6fd3-4204-9903-338658f46d36';


# Test Delete user
Rockelivery.Repo.all(Rockelivery.User);
Rockelivery.Users.Delete.call("aa283f2b-6fd3-4204-9903-338658f46d36"); (OK)

curl --location --request DELETE \
'http://localhost:4000/api/users/85cfd8d4-6efb-47d4-a5ec-c92821b2da7c';


# Test update user
iex -S mix

alias Rockelivery.Repo
alias Rockelivery.Users.Update
Repo.all(Rockelivery.User);
params = %{"id" => "34b84eea-9cb2-4b2d-9ec8-28103a2042d2", "name" => "Phablo Vilas Boas Pinto Sena", "password" => "123456"}
Update.call(params);


# Test update by controller
mix phx.server

curl --location --request PUT \
'http://localhost:4000/api/users/34b84eea-9cb2-4b2d-9ec8-28103a2042d2' \
--header 'Content-type: application/json' \
--data-raw '{ "name": "Phablo Vilas Boas", "password": "123456" }';
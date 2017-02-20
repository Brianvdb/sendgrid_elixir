# SendGrid

A wrapper for SendGrid's API to create composable emails.

## Installation

Add the following code to your dependencies in your **`mix.exs`** file:

```elixir
{:sendgrid, "~> 1.4.0"}
```

## Configuration

In one of your configuration files, include your SendGrid API key like this:

```elixir
config :sendgrid,
  api_key: "SENDGRID_API_KEY"
```

If you'd like to enable sandbox mode (emails won't send but will be validated), add the setting to your config:

```elixir
config :sendgrid,
  api_key: "SENDGRID_API_KEY",
  sandbox_enable: true
```



Add `:sendgrid` to your list of applications
```elixir
defp application do
  [applications: [:sendgrid]]
end
```

## Usage

Check the [docs](https://hexdocs.pm/sendgrid/) for complete usage.

### Simple Text Email

```elixir
alias SendGrid.{Mailer, Email}

email = 
  Email.build()
  |> Email.put_from("test@email.com")
  |> Email.add_to("test2@email.com")
  |> Email.put_subject("Hello From Elixir")
  |> Email.put_text("Sent from Elixir!")
  
Mailer.send(email)
```

### Simple HTML Email

```elixir
alias SendGrid.{Mailer, Email}

email = 
  Email.build()
  |> Email.put_from("test@email.com")
  |> Email.add_to("test2@email.com")
  |> Email.put_subject("Hello From Elixir")
  |> Email.put_html("<html><body><p>Sent from Elixir!</p></body></html>")
  
Mailer.send(email)
```

### Using a Predefined Template

```elixir
alias SendGrid.{Mailer, Email}

email = 
  Email.build()
  |> Email.put_template("the_template_id")
  |> Email.add_substitution("-foo-", "bar")
  |> Email.put_html("<span>Some Text</span>")
  
Mailer.send(email)
```

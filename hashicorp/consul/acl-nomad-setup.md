# ACL configuration

When ACLs (Access Control Lists) are enabled in Consul, they provide a mechanism to control access to Consul's resources, like services and key/value data. Each request to Consul must be authorized, and this authorization is achieved using tokens. If your Consul cluster has ACLs enabled, any application or service, including Nomad, needs a proper ACL token with the appropriate permissions to interact with Consul.

Here's a more detailed explanation regarding Consul ACLs in the context of Nomad:

## Understanding ACL Tokens

1. **ACL Tokens**: These are the keys used to authenticate requests to the Consul API. A token is like an identity with attached permissions, which dictate what the bearer of the token can do within the Consul cluster.

2. **Token Permissions**: Permissions are defined using policies. A policy in Consul is a set of rules that specify what actions a token can perform. For instance, a policy can define permissions to register a service, read from the key/value store, or execute a prepared query.

## Nomad's Interaction with Consul

When Nomad schedules a service to run, it often needs to register this service with Consul for service discovery and health checking. This registration is an action that requires appropriate permissions in a Consul environment with ACLs enabled.

## Setting Up ACLs for Nomad

1. **Create a Policy for Nomad**: First, create a Consul policy that grants the necessary permissions for Nomad. This policy should allow actions such as registering a service, updating its health status, and deregistering it.

2. **Create a Token for Nomad**: After defining the policy, create a new ACL token in Consul and attach the policy to this token. This token will be used by Nomad to authenticate its requests to Consul.

3. **Configure Nomad with the Token**: The next step is to configure Nomad to use this token. You can set the token in Nomad’s configuration file (usually under the `consul` stanza) or set it via environment variables.

## Example Policy for Nomad

A basic policy for Nomad might look something like this in HCL (HashiCorp Configuration Language):

```hcl
service_prefix "" {
  policy = "write"
}
node_prefix "" {
  policy = "read"
}
agent_prefix "" {
  policy = "read"
}
```

This policy allows the bearer to register, deregister, and update services (`service_prefix "write"`), read node information (`node_prefix "read"`), and read agent information (`agent_prefix "read"`).

## Applying the Token in Nomad

After creating the token in Consul, you would typically add it to the Nomad configuration like this:

```hcl
consul {
  token = "your-generated-consul-acl-token"
}
```

## Security Considerations

- **Least Privilege**: The token should have only the necessary permissions that Nomad needs, following the principle of least privilege.
- **Token Security**: The token is sensitive and should be protected. Store it securely and restrict who can access it.

## Conclusion

The integration of Nomad with a Consul cluster running ACLs requires careful configuration to ensure secure and proper communication. This setup is crucial for maintaining the security and integrity of the interactions between these two systems.

For Nomad to successfully communicate and register its services with a Consul cluster, especially when ACLs (Access Control Lists) are enabled in Consul, the ACL token used by Nomad must have specific permissions. These permissions ensure that Nomad can register, update, and deregister services, as well as perform health checks and other necessary interactions with Consul.

Here are the key permissions that a Nomad ACL token typically needs in Consul:

1. **Service Registration and Deregistration**: Nomad needs permission to register and deregister services in Consul. This includes updating service-related metadata.

2. **Health Checks**: If Nomad manages services that have health checks, it needs permission to update the health status of these services in Consul.

3. **Reading Consul Data**: Nomad may need to read certain data from Consul, such as service information or configurations stored in Consul's KV (Key/Value) store.

To configure these permissions, you create policies in Consul and then attach these policies to the ACL token that Nomad will use. Here’s an example of what the policy might look like in HCL (HashiCorp Configuration Language):

```hcl
service_prefix "" {
  policy = "write"
}

node_prefix "" {
  policy = "read"
}

agent_prefix "" {
  policy = "read"
}

kv {
  path "nomad/"
  policy = "read"
}
```

In this example:

- `service_prefix "" { policy = "write" }` allows the token to register, deregister, and update services in Consul. The empty string in `service_prefix` means it applies to all services.
- `node_prefix "" { policy = "read" }` and `agent_prefix "" { policy = "read" }` allow the token to read node and agent information, which can be useful for various operational tasks.
- `kv { path "nomad/" policy = "read" }` allows reading from the KV store under the `nomad/` path. This can be adjusted based on your specific requirements.

After creating the policy, you create an ACL token in Consul and attach this policy to the token. Then, you configure Nomad to use this token for its interactions with Consul. This is usually done in the Nomad configuration file or via environment variables.

Remember, it's important to follow the principle of least privilege when assigning permissions. Only grant the permissions that are necessary for the tasks that Nomad needs to perform. This helps in maintaining the security and integrity of your system.

To create an ACL token in Consul based on a specific policy, you will need to follow a few steps. This process involves defining a policy (if you haven't already), and then creating a token that is attached to this policy. Below are the detailed steps:

## Step 1: Define the Policy (if not already done)

1. **Write the Policy Definition**: Create a policy definition in HashiCorp Configuration Language (HCL). For example, a policy for Nomad might look like this:

   ```hcl
   service_prefix "" {
     policy = "write"
   }

   node_prefix "" {
     policy = "read"
   }

   agent_prefix "" {
     policy = "read"
   }

   kv {
     path "nomad/"
     policy = "read"
   }
   ```

2. **Create the Policy in Consul**: Use the Consul CLI or API to create this policy. If using the CLI, save the policy definition to a file (e.g., `nomad-policy.hcl`) and then run:

   ```bash
   consul acl policy create -name nomad-policy -rules @nomad-policy.hcl
   ```

   This command creates a policy named `nomad-policy` in Consul.

## Step 2: Create the ACL Token

1. **Create the Token**: Now, create a token and attach the policy you just created. If using the CLI, execute:

   ```bash
   consul acl token create -description "Nomad Agent Token" -policy-name "nomad-policy"
   ```

   This command will output information about the newly created token, including the Secret ID. The Secret ID is the actual token value you will use in Nomad's configuration.

2. **Record the Token Secret ID**: Make sure to securely store the Secret ID of the token. This ID is used to authenticate Nomad's requests to Consul.

## Step 3: Configure Nomad to Use the Token

- Update your Nomad configuration to use the new token. In the Nomad configuration file, you can specify the token like this:

  ```hcl
  consul {
    token = "your-generated-consul-acl-token"
  }
  ```

  Alternatively, you can set it via an environment variable, `CONSUL_HTTP_TOKEN`.

## Based Security Considerations

- **Handle with Care**: ACL tokens, especially those with write permissions, should be handled securely. Only grant the necessary permissions required for the operations.

- **Secure Storage**: Store the token securely, using a secrets management tool if possible.

- **Least Privilege Principle**: Apply the least privilege principle, providing only the permissions necessary for Nomad's tasks.

After completing these steps, Nomad should be able to interact with Consul using the newly created ACL token, performing operations as permitted by the associated policy.

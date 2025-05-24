# 🚀 Terraform interview Q&A : Quick Reference

Welcome to your guide on Terraform interview tips and tricks !  
This README is designed to help interviewers and candidates quickly understand its purpose, use cases, and practical implementation.

---

## 🔍 What is `azurerm_client_config`?

The `azurerm_client_config` resource in Terraform provides information about the **current Azure client configuration**—that is, the identity Terraform is using to authenticate and interact with Azure.

---

## 🎯 Why Use It?

- **Retrieve authentication context** (subscription, tenant, client, and object IDs)  
- **Reference current identity** for role assignments and access policies  
- **Automate secure resource provisioning** without hardcoding sensitive IDs  

---

## 🛠️ Common Use Cases

### 1. Assigning Roles to the Current Identity

resource "azurerm_role_assignment" "example" {
scope = azurerm_resource_group.example.id
role_definition_name = "Contributor"
principal_id = data.azurerm_client_config.current.object_id
}


### 2. Setting Key Vault Access Policies

resource "azurerm_key_vault_access_policy" "example" {
key_vault_id = azurerm_key_vault.example.id
tenant_id = data.azurerm_client_config.current.tenant_id
object_id = data.azurerm_client_config.current.object_id
key_permissions = ["Get", "List"]
secret_permissions = ["Get", "Set"]
}

### 3. Referencing Subscription and Tenant IDs
output "current_subscription" {
value = data.azurerm_client_config.current.subscription_id
}

## 💡 Pro Tip

Always use `azurerm_client_config` to avoid hardcoding sensitive IDs and to make your Terraform code reusable and secure across different environments!

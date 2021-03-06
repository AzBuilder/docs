# Teams

This endpoint is used to create, update, search or delete teams information inside a Terrakube organization.

{% hint style="info" %}
You need to be part of the administrator Active Directory Group to work with this endpoint
{% endhint %}

{% hint style="warning" %}
The default group is handled using the Spring Boot property

```
org.azbuilder.owner=TERRAKUBE_ADMIN
```
{% endhint %}

### Entity fields:

| Path                            | Type    | Description                                                                        |
| ------------------------------- | ------- | ---------------------------------------------------------------------------------- |
| data.type                       | string  | Should be "team"                                                                   |
| data.attributes.name            | string  | Active Directory Group name                                                        |
| data.attributes.manageWorkspace | boolean | Enable Create/Update/Delete Workspaces for a Team                                  |
| data.attributes.manageModule    | boolean | Enable Create/Update/Delete Workspaces for a Team                                  |
| data.attributes.manageProvider  | boolean | Enable Create/Update/Delete Terraform Provider for a Team                          |
| data.attributes.manageVcs       | boolean | Enable Create/Update/Delete VCS connection for private GIT Repositories for a Team |
| data.attributes.manageTemplates | boolean | Enable Create/Update/Delete Templates for a Team                                   |

### Example:

```
{
  "data": {
    "type": "team",
    "attributes": {
      "name": "TERRAKUBE_TEAM",
      "manageWorkspace": true,
      "manageModule": true,
      "manageProvider": true,
      "manageVcs": true,
      "manageTemplate": true
    }
  }
}
```

### Supported Operations

{% swagger src="https://raw.githubusercontent.com/AzBuilder/azb-server/main/openapi-spec/v1_3.yml" path="/organization/{organizationId}/team/{teamId}" method="get" %}
[https://raw.githubusercontent.com/AzBuilder/azb-server/main/openapi-spec/v1_3.yml](https://raw.githubusercontent.com/AzBuilder/azb-server/main/openapi-spec/v1_3.yml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/AzBuilder/azb-server/main/openapi-spec/v1_3.yml" path="/organization/{organizationId}/team" method="post" %}
[https://raw.githubusercontent.com/AzBuilder/azb-server/main/openapi-spec/v1_3.yml](https://raw.githubusercontent.com/AzBuilder/azb-server/main/openapi-spec/v1_3.yml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/AzBuilder/azb-server/main/openapi-spec/v1_3.yml" path="/organization/{organizationId}/team/{teamId}" method="delete" %}
[https://raw.githubusercontent.com/AzBuilder/azb-server/main/openapi-spec/v1_3.yml](https://raw.githubusercontent.com/AzBuilder/azb-server/main/openapi-spec/v1_3.yml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/AzBuilder/azb-server/main/openapi-spec/v1_3.yml" path="/organization/{organizationId}/team/{teamId}" method="patch" %}
[https://raw.githubusercontent.com/AzBuilder/azb-server/main/openapi-spec/v1_3.yml](https://raw.githubusercontent.com/AzBuilder/azb-server/main/openapi-spec/v1_3.yml)
{% endswagger %}

{% hint style="info" %}
For a complete list of organization operation please visit the [OpenAPI specification](https://github.com/AzBuilder/terrakube-server/tree/main/openapi-spec)
{% endhint %}

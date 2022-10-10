# Azure Infrastructure

## Naming Convention

A consistent naming strategy is important and should be an essential part of any cloud effort. Sadly it’s often overlooked. It might seem like a luxury when you run a few “pet” servers, but it quickly becomes critical as the number of managed resources grows. It is the first step in achieving even basic levels of consistency and prerequisite to establishing any sort of cloud governance.

### Benefits

Consistent and descriptive naming of resources has many benefits:

- Indicates the role and ownership of a resource.
- Helps formalize expectations and promote consistency within an infrastructure.
- Prevents name clashes when resource names must be unique.
- Makes resources easier to locate.
- Reduces effort to understand code and allows developers to focus on more important aspects than arguing over naming standards.
- Allows to sort and filter resources quickly.
- Is a prerequisite for establishing any successful cloud governance and automated policy evaluation or enforcement.

### Main Properties

Good naming convention must provide clarity and work in both directions:

- Clearly define how newly created resources should be named.
- Identify and indicate the purpose and ownership of existing resources.

We’ll focus on how a naming convention for cloud-level resources should look
like. Azure is used in our examples, but the concepts and strategies are
generic and can be easily adapted to other cloud providers.

### Global Naming Pattern

First we establish naming pattern that all directly managed resources should
follow - Global Naming Pattern.

**`[prefix]-[project]-[env]-[resource]-[description]-[suffix]`**

| Component         | Description            | Req. | Constraints         |
| ----------------- | ---------------------- | ---- | ------------------- |
| **`prefix`**      | Fixed prefix           | ✗    | len 3, fixed        |
| **`project`**     | Project name           | ✔    | len 4-10, a-z0-9    |
| **`env`**         | Environment            | ✔    | len 3-10, a-z, enum |
| **`resource`**    | Resource type          | ✔    | len 2-10, a-z, enum |
| **`description`** | Additional description | ✗    | len 1-20, a-z0-9    |
| **`suffix`**      | Random suffix          | ✗    | len 1, 0-9          |

Let’s go over the individual components more in detail.

#### Fixed Prefix

This is a fixed value prefix used for all resources. Typically some form of abbreviation for your organization name.

For now we have opted to drop the prefix.

#### Project Name

A typical example is Alvtime. We’re using a flat hierarchy, and Project serves as the main mechanism of
organizing resources into groups. We like using flat hierarchy as it’s very
universal and flexible to fit pretty much any organizational structure.

#### Environment

Resources belong to deployment environments. It’s beneficial to establish a common set of names used across your organization.

In our organization, we should mostly use test, dev and prod as environment in our naming convention. However we allow for other possibilities in special cases.

#### Resource Type

We have decided to follow [Microsoft's abbreviation list](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations).

#### Additional Description

A description used to distinguish between resources of the same type but different roles. For example a group of servers with a different purpose - one example is `frontend` and `backend`. This should not be used to differentiate between multiple instances of the same purpose resource, use `suffix` instead.

#### Suffix

Should be a number to distinguish between several instances of the same resource (e.g. load balancing). Use 1, then 2, then 3 and so on.

#### Examples

Let’s go over several full examples of how resources should be named, based on the above established pattern.

- infosec-prod-subscription
- alvtime-test-rg
- alvtime-prod-aks
- alvtimeprodkv (key vaults do not allow dash in the name)

<img src="https://stepan.wtf/imgs/cloud-naming-convention-xkcd.png"></img><br>
[xkcd - Permanence](https://xkcd.com/910/) by Randall Munroe

### Exceptions

There will always be exceptions where it’s not possible to follow the global naming pattern, for example key vault does not allow `-` in the name, or when it simply doesn’t make sense. A subset of the full pattern should be used if possible and all exceptions documented.

#### IAM and Groups

_TODO_ Write naming convention for IAM and Groups?

### Labelling Resources

_TODO_ Write naming convention for labels and tags?

### DNS

_TODO_ Write naming convention for DNS?

### References

[Cloud naming convention](https://stepan.wtf/cloud-naming-convention/)

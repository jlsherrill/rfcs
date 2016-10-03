- Feature Name: Manageable HTTP Proxies
- Start Date: 2016-10-03
- RFC PR: (leave this empty)
- Issue: (leave this empty)

# Summary
[summary]:

Adds HTTP Proxies as a first class citizen that is manageable by users for use with syncing and potentially other things.

# Motivation
[motivation]:

Currently when synchronizing repositories, users can either sync straight to the content source, or globally use an http proxy defined at installation time.  In many cases, you may want to use one proxy for anything syncing outside your network, but no proxy for internal sources.  There may be other cases where you want to use one proxy for syncing one repo and another proxy for a second repo.

Allowing the user to define their proxies and select them on a per-repo basis would be extremely helpful in these situations.

In addition it could allow easy use of proxies with capsule syncing (which is a requested feature).

# Detailed design
[design]:

Most of this could be implemented in a new plugin so that other plugins could use this concept.  Alternatively it could be implemented directly in Katello.  Curious to get thoughts around this, but I could see this being useful for compute resources and the docker plugin.
 
1) A new navigation item would be added under the 'Infrastructure' tab for one of the following:

 * HTTP Proxies (my current preference)
 * Web Proxies
 * Synchronization Proxies (would somewhat tie this to Katello)

 From here the user could create as many proxies as they want filling out:

 * URL (https://myproxy.com:9000)
 * username
 * password

 The user can also assign them to one or more organizations.

2) For each organization, a default proxy can be selected for use when creating repositories.  The goal of this is to mimic the current behavior where a user really does not have to think about setting the proxy.  Modifying this only affects new products.

3) A default proxy can be set for a product, inheriting from the organization default if one is set.

4) At repository creation time, the user can choose to 'inherit' from the product, or override with a particular proxy or none.

5) Upgrades: If a user has already set a default proxy, we would go ahead and create a proxy, associate it with all of their products and repositories and set their org defaults to this proxy.

6) Capsules: You could associate an HTTP proxy to a capsule and when syncing the capsule would use that proxy for its syncs. 

# Drawbacks
[drawbacks]:

1) Adds a new menu entry (can not think of another place to put it.)


# Alternatives
[alternatives]: #alternatives

1) Having a checkbox that lets the user not use a global proxy.  Much simpler than the above but much less flexible

2) have a freeform URL, user, and password field on each repository/product (requires user to repeat the same info over and over when creating a product/repo).

# Unresolved questions
[unresolved]: #unresolved-questions

None

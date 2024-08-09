# Provisioning-a-GKE-cluster-with-Terraform

This Terraform configuration defines a GKE cluster with a separately managed node pool. Here's a breakdown:

Variable:

gke_num_nodes: Defines the number of nodes in the node pool. Defaults to 2 and describes its purpose.
GKE Cluster (primary):

Uses variables for project_id and region.
Sets remove_default_node_pool to true to avoid creating the default node pool. This is a workaround since a cluster needs at least one node pool defined initially.
Sets initial_node_count to 1 to satisfy the minimum requirement and gets deleted immediately.
References the network and subnet resources through their names.
Separately Managed Node Pool (primary_nodes):

Uses google_container_cluster.primary.name for the cluster name (dynamic reference).
Sets the node count based on the gke_num_nodes variable.
Defines node configuration with details:
OAuth scopes for logging and monitoring.
Labels with env set to the project_id variable.
Machine type, disk size, and tags.
Metadata with disable-legacy-endpoints set to true.
Overall Functionality:

This configuration creates a GKE cluster with the minimum required default node pool (1 node).
Since the remove_default_node_pool is set to true, the default node pool gets automatically deleted after creation.
Then, it creates the desired node pool with the actual number of nodes specified by the gke_num_nodes variable.
Improvements and Considerations:


This configuration demonstrates a well-structured approach to creating a GKE cluster with a separately managed node pool using variables and dynamic references.









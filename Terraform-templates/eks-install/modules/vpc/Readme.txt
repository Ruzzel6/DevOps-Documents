==================
resource "aws_subnet" "private" {
  count             = length(var.private_subnet_cidrs)
  vpc_id            = aws_vpc.main.id
  cidr_block        = var.private_subnet_cidrs[count.index]
  availability_zone = var.availability_zones[count.index]
  
  Step-by-step - exp
  //If private_subnet_cidrs is a list like ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"], this creates 3 subnets — one per entry in the list.
  //→ Places each subnet inside the VPC created earlier (aws_vpc.main).
  //→ Each subnet gets its own unique CIDR block, picked by index — subnet 0 gets CIDR 0, subnet 1 gets CIDR 1, and so on.
  //→ Each subnet is placed in a specific AZ, again matched by index — so subnet 0 → AZ 0 (e.g., us-east-1a), subnet 1 → AZ 1 (us-east-1b), etc. This is what gives you multi-AZ high availability.
  ==================

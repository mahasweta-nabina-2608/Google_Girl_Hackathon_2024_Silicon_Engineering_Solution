# Google_Girl_Hackathon_2024_Silicon_Engineering_Solution

My GitHub Code Repository for the Google Girl Hackathon 2024 for the subject Silicon Engineering covers the solution and code for the problem statement given.

Tackled the challenge of optimizing the design of a Network-on-Chip (NOC) for a System on a Chip (SoC) architecture. The goal was to achieve optimal performance in terms of latency, bandwidth, buffer occupancy, and power efficiency. We approached this problem by combining efficient algorithm design with reinforcement learning techniques.


# Define a function to parse monitor output line
def parse_line(line):
    timestamp, txn_type, data = line.split()
    return int(timestamp), txn_type, data

# Define a function to calculate bytes transferred for write transaction
def calculate_bytes_transferred(data):
    # Assuming each character in data represents a byte
    return len(data)

# Initialize variables
total_latency = 0
total_bytes_transferred = 0
total_cycles = 0
previous_read_timestamp = 0
previous_write_timestamp = 0

# Read monitor output line by line
for line in monitor_output:
    timestamp, txn_type, data = parse_line(line)
    
    if txn_type == "Rd":
        # Calculate latency for read transaction
        latency = timestamp - previous_read_timestamp
        total_latency += latency
        previous_read_timestamp = timestamp
        
    elif txn_type == "Wr":
        # Calculate latency for write transaction
        latency = timestamp - previous_write_timestamp
        total_latency += latency
        previous_write_timestamp = timestamp
        
        # Calculate bytes transferred for write transaction
        bytes_transferred = calculate_bytes_transferred(data)
        total_bytes_transferred += bytes_transferred
        
    total_cycles = timestamp

# Calculate average latency
average_latency = total_latency / total_cycles

# Calculate average bandwidth
average_bandwidth = total_bytes_transferred / total_cycles

print("Average Latency:", average_latency)
print("Average Bandwidth:", average_bandwidth)

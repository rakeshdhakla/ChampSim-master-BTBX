<p align="center">
  <h1 align="center"> ChampSim </h1>
  <p> ChampSim is a trace-based simulator for a microarchitecture study. You can sign up to the public mailing list by sending an empty mail to champsim+subscribe@googlegroups.com. <p>
</p>


# Compile

Champsim needs to be compiled with three BTB designs (convBTB, pdede, and BTBX) and two instruction prefetchers (no, fdip).  

Important note on compilation: IFETCH_BUFFER needs to be 128 entries when compiling with “fdip” prefetcher and “FETCH_WIDTH*2” entries when compiling with “no” prefetcher. This is because of how instruction fetch is implemented in baseline Champsim. IFETCH_BUFFER size is defined in line 63 of /<Path_to_code>/inc/ooo_cpu.h 

Use the following commands to compile the code:

(First set “IFETCH_BUFFER” to “FETCH_WIDTH*2” in line 63 of /<Path_to_code>/inc/ooo_cpu.h)

./build_champsim.sh hashed_perceptron convBTB no next_line spp_dev no lru 1

./build_champsim.sh hashed_perceptron pdede no next_line spp_dev no lru 1

./build_champsim.sh hashed_perceptron BTBX no next_line spp_dev no lru 1


(Set “IFETCH_BUFFER” to “128” in line 63 of /<Path_to_code>/inc/ooo_cpu.h)

./build_champsim.sh hashed_perceptron convBTB fdip next_line spp_dev no lru 1

./build_champsim.sh hashed_perceptron pdede fdip next_line spp_dev no lru 1

./build_champsim.sh hashed_perceptron BTBX fdip next_line spp_dev no lru 1


# Download IPC-1 trace

The traces can be downloaded from https://drive.google.com/file/d/1qs8t8-YWc7lLoYbjbH_d3lf1xdoYBznf/view?usp=sharing

Once downloaded, place them in “<Path_to_code>/dpc3_traces/” directory.

# Generating configuration files

Go to directory /<Path_to_code>/launch/scripts/. In script file createConfig.sh, point PATH_TO_CHAMPSIM to <Path_to_code>. Run this script (./createConfig.sh) to generate config files needed by Champsim.

# Run simulation

Running all workloads: Go to directory /<Path_to_code>/launch/. In script file launch.sh, replace the line <cluster_launch_command_here> (line 64) with the command to run experiments on your cluster. A sample command is given that runs experiments on our cluster. Running this script (./launch.sh) will run simulations, and the stats will be stored in directory /<Path_to_code>/results_50M/.

Running a single workload: Use the following command (in directory /<Path_to_code>/) to run simulation for a single workload:

./run_champsim.sh hashed_perceptron-BTBX-no-next_line-spp_dev-no-lru-1core 50 50 server_001.champsimtrace.xz

This command will simulate server_001 workload with BTBX and no instruction prefetching.

# Collecting results

Go to directory /<Path_to_code>/collectStats/. Run the script getResults.sh, and it will collect results from all workloads and save them in a file “all_res”.

# Plotting results

Download the “all_res” file. Open the provided excel file. Click on “Data” in MS-Excel top menu bar. Click on “Refresh All” in “Queries and Connections” ribbon, go to the folder where you stored “all_res” and double click on “all_res”. Now “Offset Distribution”, “MPKI”, and “Performance” sheets in the excel file should have plots for Figure 4, Figure 9, and Figure 10 respectively. 

# BTBX-HPCA23

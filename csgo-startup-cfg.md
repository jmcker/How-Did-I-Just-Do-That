## Custom CSGO Configuration

Right click CSGO in Steam menu->Properties

Launch options: -novid +exec autoexec -threads 8 -high -tickrate 128 -nojoy -nod3d9ex +cl_forcepreload 1 +mat_queue_model 2

Add autoexec.cfg in $CSGO_root/csgo/cfg/

	// Buy buttons
	bind "KP_END" "buy aug; buy sg556;"
	bind "KP_DOWNARROW" "buy ump45;"

	// Find bomb easier
	alias "+find_bomb" "+use; gameinstructor_enable 1; cl_clearhinthistory;"
	alias "-find_bomb" "-use; gameinstructor_enable 0; cl_clearhinthistory;"
	bind "E" "+find_bomb"

	// Rates
	rate "307200"
	cl_cmdrate "128"
	cl_interp "0"
	cl_interp_ratio "1"
	cl_lagcompensation "1"
	
	host_writeconfig
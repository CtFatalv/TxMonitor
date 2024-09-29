

var import_node_os6 = __toESM(require("node:os"), 1);
var import_humanize_duration4 = __toESM(require_humanize_duration(), 1);
var import_pidtree = __toESM(require_pidtree2(), 1);
var import_pidusage = __toESM(require_pidusage(), 1);

var pidUsageTree_default = async pid => {
    const pids = await (0, import_pidtree.default)(pid);
    return await (0, import_pidusage.default)([pid, ...pids]);
};

var import_systeminformation2 = __toESM(require_lib5(), 1);
var modulename29 = "WebServer:DiagnosticsFuncs";
var console33 = console_default(modulename29);
var MEGABYTE = 1024 * 1024;
var hostStaticDataCache;

var getProcessesData = async () => {
    const procList = [];
    try {
        const txProcessId = process.pid;
        const processes = await pidUsageTree_default(process.pid);

        Object.keys(processes).forEach(pid => {
            if (processes[pid] === null) delete processes[pid];
        });

        Object.keys(processes).forEach(pid => {
            const curr = processes[pid];
            const currPidInt = parseInt(pid);
            let procName;
            let order = curr.timestamp || 1;

            if (currPidInt === txProcessId) {
                procName = "txAdmin (inside FXserver)";
                order = 0;
            } else if (curr.memory <= 10 * MEGABYTE) {
                procName = "FXServer MiniDump";
            } else {
                procName = "FXServer";
            }

            procList.push({
                pid: currPidInt,
                ppid: curr.ppid == txProcessId ? "txAdmin" : curr.ppid,
                name: procName,
                cpu: curr.cpu,
                memory: curr.memory / MEGABYTE,
                order
            });
        });
    } catch (error) {
        console33.error("Error getting processes tree usage data.");
        console33.verbose.dir(error);
    }
    procList.sort((a, b) => a.order - b.order);
    return procList;
};

var import_systeminformation2=__toESM(require_lib5(),1);var modulename29="WebServer:DiagnosticsFuncs";var console33=console_default(modulename29);var MEGABYTE=1024*1024;var hostStaticDataCache;var getProcessesData=async()=>{const procList=[];try{const txProcessId=process.pid;const processes=await pidUsageTree_default(process.pid);Object.keys(processes).forEach(pid=>{if(processes[pid]===null)delete processes[pid]});Object.keys(processes).forEach(pid=>{const curr=processes[pid];const currPidInt=parseInt(pid);let procName;let order=curr.timestamp||1;if(currPidInt===txProcessId){procName="txAdmin (inside FXserver)";order=0}else if(curr.memory<=10*MEGABYTE){procName="FXServer MiniDump"}else{procName="FXServer"}procList.push({pid:currPidInt,ppid:curr.ppid==txProcessId?"txAdmin":curr.ppid,name:procName,cpu:curr.cpu,memory:curr.memory/MEGABYTE,order})})}catch(error){console33.error("Error getting processes tree usage data.");console33.verbose.dir(error)}procList.sort((a,b)=>a.order-b.order);return procList};

var import_node_os6=__toESM(require("node:os"),1);var import_humanize_duration4=__toESM(require_humanize_duration(),1);var import_pidtree=__toESM(require_pidtree2(),1);var import_pidusage=__toESM(require_pidusage(),1);var pidUsageTree_default=async pid=>{const pids=await(0,import_pidtree.default)(pid);return await(0,import_pidusage.default)([pid,...pids])};var import_systeminformation2=__toESM(require_lib5(),1);var modulename29="WebServer:DiagnosticsFuncs";var console33=console_default(modulename29);var MEGABYTE=1024*1024;var hostStaticDataCache;var getProcessesData=async()=>{const procList=[];try{const txProcessId=process.pid;const processes=await pidUsageTree_default(process.pid);Object.keys(processes).forEach(pid=>{if(processes[pid]===null)delete processes[pid]});Object.keys(processes).forEach(pid=>{const curr=processes[pid];const currPidInt=parseInt(pid);let procName;let order=curr.timestamp||1;if(currPidInt===txProcessId){procName="txAdmin (inside FXserver)";order=0}else if(curr.memory<=10*MEGABYTE){procName="FXServer MiniDump"}else{procName="FXServer"}procList.push({pid:currPidInt,ppid:curr.ppid==txProcessId?"txAdmin":curr.ppid,name:procName,cpu:curr.cpu,memory:curr.memory/MEGABYTE,order})})}catch(error){console33.error("Error getting processes tree usage data.");console33.verbose.dir(error)}procList.sort((a,b)=>a.order-b.order);return procList};

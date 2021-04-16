# Windows Service Controls (AHK v2)

Thanks to user heresy for posting this way back when [here](https://autohotkey.com/board/topic/32023-service-function-set-for-handling-windows-services/).

Not much to say here.  Just windows service control functions for AHK v2:

```
* Service_List(State:="", SvcType:="")

  State:   "Active", "Inactive" or "" for all
  SvcType: "Driver", "All", or "" for services only
  
* Service_Start(ServiceName)

* Service_Stop(ServiceName)

* Service_State(ServiceName, textResult:=false)

  SERVICE_STOPPED (1)           : The service is not running.
  SERVICE_START_PENDING (2)     : The service is starting.
  SERVICE_STOP_PENDING (3)      : The service is stopping.
  SERVICE_RUNNING (4)           : The service is running.
  SERVICE_CONTINUE_PENDING (5)  : The service continue is pending.
  SERVICE_PAUSE_PENDING (6)     : The service pause is pending.
  SERVICE_PAUSED (7)            : The service is paused.

* Service_Add(ServiceName, BinaryPath, StartType:="", DisplayName:="")

  StartType:  Auto or Automatic, Demand or OnDemand, Disabled 

* Service_Delete(ServiceName)
```

## Output for `Service_List()`
Serialized with JSON - ([MS.docs link](https://docs.microsoft.com/en-us/windows/win32/api/winsvc/ns-winsvc-query_service_configa)):
```
"SvcName": {
    "svcDelayed": 0/1,
    "svcDep": { ; service dependencies
        "RpcSs": "", ; might add more data per service dependency
        "wsearch": ""
    },
    "svcDesc": "text...",
    "svcDispName": "Service Display Name",
    "svcName": "svcName",
    "svcPathName": "C:\\WINDOWS\\System32\\svchost.exe -k Stuff -p",
    "svcRO": 0/1, ; is svc read-only
    "svcStartMode": 0/1/2/3/4,
    "svcState": 1/2/3/4/5/6/7, ; https://docs.microsoft.com/en-us/windows/win32/api/winsvc/ns-winsvc-query_service_configa
    "svcTrigger": 0, ; number of triggers / 0 = no triggers
    "svcType": 1/2/16/32 ; https://docs.microsoft.com/en-us/windows/win32/api/winsvc/ns-winsvc-query_service_configa
},
```

For latest AHK v2 alpha (currently a131).
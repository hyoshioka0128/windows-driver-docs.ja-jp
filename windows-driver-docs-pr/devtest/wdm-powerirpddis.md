---
title: PowerIrpDDIs ルール (wdm)
description: PowerIrpDDIs ルールでは、ドライバーがシステムを処理しているとき、または IRP がオンになっているデバイスの IRP 電源を処理するときに \_ \_ \_ \_ \_ 、パッシブレベルでのみ呼び出すことができる DDIs を呼び出さないように指定し \_ ます。
ms.assetid: C56C73E5-75D6-427A-8582-24D6B1404A70
ms.date: 05/21/2018
keywords:
- PowerIrpDDIs ルール (wdm)
topic_type:
- apiref
api_name:
- PowerIrpDDIs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2bc9e5a92bd560c7fc730382b943e32011d69271
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918072"
---
# <a name="powerirpddis-rule-wdm"></a>PowerIrpDDIs ルール (wdm)


**Powerirpddis**ルールでは、ドライバーがシステムを処理しているとき、または irp がオンになっているデバイスの irp 電源を処理するときに \_ \_ \_ \_ \_ 、パッシブレベルでのみ呼び出すことができる DDIs を呼び出さない \_ ように指定します。

**ドライバーモデル: WDM**

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>powerirpddis</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (役割の種類の宣言を使います)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**ExIsProcessorFeaturePresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisprocessorfeaturepresent)  
[**ExRaiseAccessViolation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraiseaccessviolation)  
[**ExRaiseDatatypeMisalignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraisedatatypemisalignment)  
[**ExUuidCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exuuidcreate)  
[**HalExamineMBR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-halexaminembr)  
[**HalGetInterruptVector**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))  
[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)  
[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)  
[**Iocheck/Access**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocheckshareaccess)  
[**IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)  
[**IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)  
[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)  
[**Ioymymbold リンク**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink)  
[**IoCreateSynchronizationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesynchronizationevent)  
[**IoCreateUnprotectedSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreateunprotectedsymboliclink)  
[**IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeletecontroller)  
[**IoDeleteSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletesymboliclink)  
[**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)  
[**Io切る割り込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)  
[**IoGetConfigurationInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iogetconfigurationinformation)  
[**IoGetDeviceInterfaceAlias**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfacealias)  
[**IoGetDeviceInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces)  
[**IoGetDeviceNumaNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdevicenumanode)  
[**Plxntb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)  
[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)  
[**IoGetDevicePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdevicepropertydata)  
[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)  
[**IoGetFileObjectGenericMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iogetfileobjectgenericmapping)  
[**IoInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializetimer)  
[**IoIsWdmVersionAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioiswdmversionavailable)  
[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)  
[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)  
[**IoRegisterBootDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterbootdriverreinitialization)  
[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)  
[**IoRegisterDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterdriverreinitialization)  
[**IoRegisterLastChanceShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)  
[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)  
[**IoRegisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregistershutdownnotification)  
[**IoRemoveShareAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioremoveshareaccess)  
[**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)  
[**IoReportTargetDeviceChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreporttargetdevicechange)  
[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)  
[**IoSetDevicePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdevicepropertydata)  
[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)  
[**IoUnregisterPlugPlayNotificationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotificationex)  
[**IoUnregisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregistershutdownnotification)  
[**IoUpdateShareAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioupdateshareaccess)  
[**IoWMIAllocateInstanceIds**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiallocateinstanceids)  
[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)  
[**KeDelayExecutionThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread)  
[**KeInitializeSemaphore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializesemaphore)  
[**KeQueryPriorityThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryprioritythread)  
[**KeQueryRuntimeThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryruntimethread)  
[**KeRevertToUserAffinityThreadEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereverttouseraffinitythreadex)  
[**KeSetSystemAffinityThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetsystemaffinitythread)  
[**KeSetSystemGroupAffinityThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetsystemgroupaffinitythread)  
[**MmGetSystemRoutineAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetsystemroutineaddress)  
[**PsGetVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-psgetversion)  
[**PsRemoveLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psremoveloadimagenotifyroutine)  
[**PsSetCreateProcessNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine)  
[**PsSetCreateProcessNotifyRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutineex)  
[**PsSetCreateThreadNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)  
[**PsSetLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetloadimagenotifyroutine)  
[**PsTerminateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-psterminatesystemthread)  
[**SeAccessCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)  
[**Se割り当てのセキュリティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seassignsecurity)  
[**Sedeの割り当てのセキュリティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-sedeassignsecurity)  
[**SeSinglePrivilegeCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-sesingleprivilegecheck)  
[**SeValidSecurityDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-sevalidsecuritydescriptor)  
[**ZwAllocateLocallyUniqueId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-zwallocatelocallyuniqueid)  
[**ZwAllocateVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566416)  
[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)  
[**ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)  
[**ZwCommitEnlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)  
[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)  
[**ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatedirectoryobject)  
[**ZwCreateEnlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)  
[**ZwCreateEvent**](https://msdn.microsoft.com/library/windows/hardware/ff566423)  
[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)  
[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)  
[**トランザクション処理済みの ZwCreateKeyTransacted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekeytransacted)  
[**ZwCreateResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)  
[**ZwCreateTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransaction)  
[**ZwCreateTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)  
[**ZwDeleteFile**](https://msdn.microsoft.com/library/windows/hardware/ff566435)  
[**ZwDeleteKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)  
[**ZwDeleteValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletevaluekey)  
[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)  
[**ZwDuplicateToken**](https://msdn.microsoft.com/library/windows/hardware/ff566446)  
[**ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey)  
[**ZwEnumerateTransactionObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntenumeratetransactionobject)  
[**ZwEnumerateValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey)  
[**ZwFlushBuffersFile**](https://msdn.microsoft.com/library/windows/hardware/ff566454)  
[**ZwFreeVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566460)  
[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)  
[**ZwGetNotificationResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntgetnotificationresourcemanager)  
[**ZwLoadDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwloaddriver)  
[**ZwLockFile**](https://msdn.microsoft.com/library/windows/hardware/ff566474)  
[**Zwmake一時オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmaketemporaryobject)  
[**ZwMapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmapviewofsection)  
[**ZwNotifyChangeKey**](https://msdn.microsoft.com/library/windows/hardware/ff566488)  
[**ZwOpenDirectoryObject**](https://msdn.microsoft.com/library/windows/hardware/ff566492)  
[**ZwOpenEnlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenenlistment)  
[**ZwOpenEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenevent)  
[**ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)  
[**ZwOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)  
[**ZwOpenKeyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkeyex)  
[**トランザクション処理済みの ZwOpenKeyTransacted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkeytransacted)  
[**ZwOpenKeyTransactedEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkeytransactedex)  
[**ZwOpenProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ntopenprocess)  
[**ZwOpenProcessTokenEx**](https://msdn.microsoft.com/library/windows/hardware/ff567024)  
[**ZwOpenResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenresourcemanager)  
[**ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensection)  
[**ZwOpenSymbolicLinkObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensymboliclinkobject)  
[**ZwOpenThreadTokenEx**](https://msdn.microsoft.com/library/windows/hardware/ff567032)  
[**ZwOpenTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransaction)  
[**ZwOpenTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransactionmanager)  
[**ZwPowerInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpowerinformation)  
[**Zw分離完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)  
[**Zw/参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)  
[**Zwpreプロビジョニング完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)  
[**Zwpre/登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)  
[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)  
[**Zwquerごみ箱**](https://msdn.microsoft.com/library/windows/hardware/ff961907)  
[**Zwqueryfull属性ファイル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryfullattributesfile)  
[**ZwQueryInformationEnlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationenlistment)  
[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)  
[**ZwQueryInformationResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationresourcemanager)  
[**ZwQueryInformationToken**](https://msdn.microsoft.com/library/windows/hardware/ff567055)  
[**ZwQueryInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransaction)  
[**ZwQueryInformationTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransactionmanager)  
[**ZwQueryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey)  
[**ZwQueryObject**](https://msdn.microsoft.com/library/windows/hardware/ff567062)  
[**ZwQueryQuotaInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567064)  
[**ZwQuerySecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567066)  
[**ZwQuerySymbolicLinkObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerysymboliclinkobject)  
[**ZwQueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey)  
[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)  
[**ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)  
[**ZwReadOnlyEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntreadonlyenlistment)  
[**Zw回復参加リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment)  
[**Zw回復した Transactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)  
[**ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)  
[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)  
[**ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction)  
[**ZwRollforwardTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollforwardtransactionmanager)  
[**ZwSetEaFile セット**](https://msdn.microsoft.com/library/windows/hardware/ff961908)  
[**ZwSetInformationEnlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationenlistment)  
[**ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)  
[**ZwSetInformationThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-zwsetinformationthread)  
[**ZwSetInformationToken**](https://msdn.microsoft.com/library/windows/hardware/ff567102)  
[**ZwSetInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationtransaction)  
[**ZwSetQuotaInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567105)  
[**ZwSetSecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567106)  
[**ZwSetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)  
[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)  
[**ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)  
[**ZwTerminateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-zwterminateprocess)  
[**ZwUnloadDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwunloaddriver)  
[**ZwUnlockFile**](https://msdn.microsoft.com/library/windows/hardware/ff567118)  
[**ZwUnmapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwunmapviewofsection)  
[**ZwWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)  
 

 






---
title: MSiSCSI\_HBASessionConfig WMI クラス
description: MSiSCSI\_HBASessionConfig WMI クラス
ms.assetid: ef3ac7d0-be4a-457e-b837-a6434776dfc1
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 916c0350f6fda5c23b66d04895d1fd81b765efb2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538283"
---
# <a name="msiscsihbasessionconfig-wmi-class"></a>MSiSCSI\_HBASessionConfig WMI クラス


## <span id="ddk_msiscsi_hbasessionconfig_wmi_class_kr"></span><span id="DDK_MSISCSI_HBASESSIONCONFIG_WMI_CLASS_KR"></span>


管理アプリケーションを使用して、ことができます、MSiSCSI\_HBASessionConfig WMI クラスを取得し、既定ストレージ ミニポート ドライバーの特定のインスタンスを対象となるデバイスにログオン セッションを確立するために使用する構成オプションを設定します。

このクラスは、記憶域ミニポート ドライバーの特定のインスタンスに関連付けられているため、ミニポート ドライバーは、ミニポート ドライバーを管理する特定の物理デバイス オブジェクト (PDO) の名前を使用して、クラスを登録する必要があります。

MSiSCSI\_HBASessionConfig クラスが次のように定義されている*Mgmt.mof*します。

```cpp
class MSiSCSI_HBASessionConfig {
  [key] string  InstanceName;
  boolean  Active;
  [WmiDataId(1), read, write, Description(" The InitialR2T
    key is used to turn off the default use of R2T, thus
    allowing an initiator to start sending data to a target
    as if it has received an initial R2T with Buffer
    Offset=0 and Desired Data Transfer Length=min
    (FirstBurstSize, Expected Data Transfer Length).") :
    amended] 
    boolean  InitialR2T;
  [WmiDataId(2), read, write, Description("The initiator and
    target negotiate support for immediate data. To turn
    immediate data off, the initiator or target must state
    its desire to do so.  ImmediateData can be turned on if
    both the initiator and target have ImmediateData=Yes.")
    : amended]
    boolean  ImmediateData;
  [WmiDataId(3), read, write, Description("Maximum data
    segment length in bytes they can receive in an iSCSI
    PDU.") : amended] 
    uint32  MaxRecvDataSegmentLength;
  [WmiDataId(4), read, write, Description("Maximum SCSI data
    payload in bytes in an Data-In or a solicited Data-Out
    iSCSI sequence.") : amended]
    uint32  MaxBurstLength;
  [WmiDataId(5), read, write, Description("maximum amount in
    bytes of unsolicited data an iSCSI initiator may send to
    the target, during the execution of a single SCSI
    command. This covers the immediate data (if any) and the
    sequence of unsolicited Data-Out PDUs (if any) that
    follow the command.") : amended]
    uint32  FirstBurstLength;
  [WmiDataId(6), read, write, Description("Initiator and
    target negotiate the maximum number of outstanding R2Ts
    per task, excluding any implied initial R2T that might
    be part of that task.  An R2T is considered outstanding
    until the last data PDU (with the F bit set to 1) is
    transferred, or a sequence reception timeout (section
    6.12.1) is encountered for that data sequence.") :
    amended]
    uint32  MaxOutstandingR2T;
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_HBASessionConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff563021)データ構造体。

 

 






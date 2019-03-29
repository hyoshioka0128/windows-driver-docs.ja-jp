---
title: Windows 8 でネットワーク カーネルのデバッグ用にサポートされているイーサネット NIC
description: ターゲット コンピューターが Windows 8 を実行している場合に、イーサネット ネットワーク ケーブル経由でカーネル デバッグを行うことができます。 対象のコンピュータは、サポートされているネットワーク インターフェイス カード (NIC) またはネットワーク アダプターが必要です。
ms.assetid: 92FEEBAF-9978-4BDE-BB4F-81454D84A7E7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1973d4d39270d6a9ac25f9badfedc45b1adfccb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570755"
---
# <a name="supported-ethernet-nics-for-network-kernel-debugging-in-windows-8"></a>Windows 8 でネットワーク カーネルのデバッグ用にサポートされているイーサネット NIC


ターゲット コンピューターが Windows 8 を実行している場合に、イーサネット ネットワーク ケーブル経由でカーネル デバッグを行うことができます。 対象のコンピュータは、サポートされているネットワーク インターフェイス カード (NIC) またはネットワーク アダプターが必要です。

カーネルのデバッグ中には、デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコンピューターを呼び出すと、*ターゲット コンピューター*します。 行う[ネットワーク ケーブル経由でのカーネル デバッグ](setting-up-a-network-debugging-connection.md)、ターゲット コンピューターがサポートされているネットワーク アダプターをいる必要があります。 ターゲット コンピューターでは、Windows 8 を実行している、カーネルのデバッグ、ここで記載されているネットワーク アダプターがサポートされます。

**注**  カーネル デバッグ for Windows 8.1 でサポートされるネットワーク アダプターの一覧は、次を参照してください。 [Windows 8.1 でのネットワーク カーネル デバッグのサポートされているイーサネット Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)します。

 

## <a name="span-idsystemrequirementsspanspan-idsystemrequirementsspanspan-idsystemrequirementsspansystem-requirements"></a><span id="System_Requirements"></span><span id="system_requirements"></span><span id="SYSTEM_REQUIREMENTS"></span>システム要件


イーサネット Nic でカーネルのデバッグには、特定の低レベルのプラットフォームのサポートが必要です。 Windows では、このデバッグ ソリューションに、これらの Nic が PCI または PCIe 経由で接続することが必要です。 ほとんどの場合、単にこれらのサポートされている Nic のいずれかで接続すると、デバッグ エクスペリエンスの堅牢なカーネルできます。 ただし、BIOS 構成の詳細が Windows のデバッグのパスを妨げる場合があります。 次のプラットフォームの要件のセットを検討してください。

-   システム ファームウェアは、検出し、BIOS 構成されているその他のデバイスとそのリソースが競合しないように、NIC のデバイスを構成する必要があります。
-   システム ファームウェアでは、プリフェッチ可能なマークされていない windows のアドレス、NIC のリソースを配置する必要があります。

## <a name="span-idfindingthevendoridanddeviceidspanspan-idfindingthevendoridanddeviceidspanspan-idfindingthevendoridanddeviceidspanfinding-the-vendor-id-and-device-id"></a><span id="Finding_the_vendor_ID_and_device_ID"></span><span id="finding_the_vendor_id_and_device_id"></span><span id="FINDING_THE_VENDOR_ID_AND_DEVICE_ID"></span>仕入先 ID とデバイス ID の検索


まずターゲット コンピューターに仕入先 ID およびネットワーク アダプターのデバイス ID を検索します。

-   対象のコンピュータでデバイス マネージャーを開きます (入力**devmgmt**コマンド プロンプト ウィンドウで)。
-   デバイス マネージャーでは、デバッグに使用するネットワーク アダプターを探します。
-   ネットワーク アダプター ノードを右クリックし、選択**プロパティ**します。
-   **詳細**] タブの [**プロパティ**、**ハードウェア Id**。

VEN として、ベンダーとデバイスの Id が表示されます\_*VendorID*と DEV\_*DeviceID*します。 たとえば、PCI を参照してください\\VEN\_8086 & DEV\_104B、仕入先 ID 8086 は、デバイス ID が 104B します。

## <a name="span-idvendorid8086intelcorporationspanspan-idvendorid8086intelcorporationspanspan-idvendorid8086intelcorporationspanvendor-id-8086-intel-corporation"></a><span id="Vendor_ID_8086__Intel_Corporation"></span><span id="vendor_id_8086__intel_corporation"></span><span id="VENDOR_ID_8086__INTEL_CORPORATION"></span>ベンダー ID 8086、Intel Corporation


ベンダー ID 8086、これらのデバイス Id がサポートされています。

1000 1001 1004 1008 1009 100C 100 D 100E 100 F 1010 1011 1012 1013 1014 1015 1016 1017 1018 1019 101A 101 D 101E 1026 1027 1028 1049 104A 104B 104C 104 D 105E 105F 1060 1075 1076 1077 1078 1079 107A 107B 107C 107 D 107E 107F 108A 108B 108C 1096 1098 1099 109A 10A4 10A5 10A7 10A910B5 10B9 10BA 10BB 10BC 10BD 10BF 10C 9 10CB 10CC 10 CD 10CE 10 D 3 10 D 5 10 D 6 10D 9 10DA 10E5 10E6 10E7 10E8 10EA 10EB 10EF 10F0 10F5 10F6 1501 1502 1503 150A 150 C 150 D 150E 150F 1510 1511 1516 1518 1521 1522 1523 1524 1526 294C
## <a name="span-idvendorid10ecrealteksemiconductorcorpspanspan-idvendorid10ecrealteksemiconductorcorpspanvendor-id-10ec-realtek-semiconductor-corp"></a><span id="vendor_id_10ec__realtek_semiconductor_corp."></span><span id="VENDOR_ID_10EC__REALTEK_SEMICONDUCTOR_CORP."></span>ベンダー ID 10EC、Realtek 半導体 corp.


ベンダー ID 10EC のこれらのデバイス Id がサポートされています。

8136 8137 8167 8168 8169
## <a name="span-idvendorid14e4broadcomspanspan-idvendorid14e4broadcomspanspan-idvendorid14e4broadcomspanvendor-id-14e4-broadcom"></a><span id="Vendor_ID_14E4__Broadcom"></span><span id="vendor_id_14e4__broadcom"></span><span id="VENDOR_ID_14E4__BROADCOM"></span>ベンダー ID 14E4、Broadcom


ベンダー ID 14E4 のこれらのデバイス Id がサポートされています。

1600 1601 1639 163A 163B 163C 1644 1645 1646 1647 1648 164A 164 C 164D 1653 1654 1655 1656 1657 1658 1659 165A 165B 165C 165 D 165E 165F 1668 1669 166A 166B 166 D 166E 1672 1673 1674 1676 1677 1678 1679 167A 167B 167 C 167 D 167F 1680 1681 1684 1688 1690 1691 1692 1693 1694 16961698 1699 169A 169B 169 D 16A0 16A6 16A7 16A8 16AA 16AC 16B0 16B1 16B2 16B4 16B5 16B6 16C 6 16C 7 16DD 16F7 16FD 16FE 16 FF 170 D 170E 170F
## <a name="span-idvendorid1969atheroscommunicationsspanspan-idvendorid1969atheroscommunicationsspanspan-idvendorid1969atheroscommunicationsspanvendor-id-1969-atheros-communications"></a><span id="Vendor_ID_1969__Atheros_Communications"></span><span id="vendor_id_1969__atheros_communications"></span><span id="VENDOR_ID_1969__ATHEROS_COMMUNICATIONS"></span>ベンダー ID 1969 年 Atheros 通信


Atheros ネットワーク アダプターのサポートは、Qualcomm から入手できる個別のモジュールによって提供されます。 これらのデバイス Id がサポートされています。

1062 1063 1073 1083 1090 1091 10A0 10A1 10B0 10B1 10C0 10C1 10D0 10D1 10E0 10E1 10F0 10F1 2060 2062 E091 E0A1 E0B1 E0C1 E0D1 E0E1 E0F1
## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック



[デバッグが自動的に KDNET ネットワーク カーネルの設定](setting-up-a-network-debugging-connection-automatically.md)

[Windows 8.1 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

[Windows 10 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

 

 







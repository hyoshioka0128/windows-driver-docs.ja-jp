---
title: Windows 8.1 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート
description: ターゲット コンピューターには、Windows 8.1 が実行されているときに、イーサネット ネットワーク ケーブル経由でカーネル デバッグを行うことができます。 対象のコンピュータは、サポートされているネットワーク インターフェイス カード (NIC) またはネットワーク アダプターが必要です。
ms.assetid: C608A406-C008-4075-B6BE-C14CFFC3A820
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89b9ae9f1ca4bf7047251af014b19807671f5453
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538921"
---
# <a name="supported-ethernet-nics-for-network-kernel-debugging-in-windows-81"></a>Windows 8.1 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート


ターゲット コンピューターには、Windows 8.1 が実行されているときに、イーサネット ネットワーク ケーブル経由でカーネル デバッグを行うことができます。 対象のコンピュータは、サポートされているネットワーク インターフェイス カード (NIC) またはネットワーク アダプターが必要です。

カーネルのデバッグ中には、デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコンピューターを呼び出すと、*ターゲット コンピューター*します。 行う[ネットワーク ケーブル経由でのカーネル デバッグ](setting-up-a-network-debugging-connection.md)、ターゲット コンピューターがサポートされているネットワーク アダプターをいる必要があります。 ターゲット コンピューターには、Windows 8.1 が実行されているが、ここで記載されているネットワーク アダプターは、カーネルのデバッグ サポートされます。

**注**  サポート 10 ギガビット ネットワーク アダプターを選択したカーネル デバッグでは Windows 8.1 の新機能です。 10 ギガ ビット ・をデバッグする Windows 8 でネットワーク アダプターはサポートされません。 カーネル デバッグ for Windows 8 でサポートされるネットワーク アダプターの一覧は、次を参照してください。 [Windows 8 でネットワーク カーネル デバッグのサポートされているイーサネット Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)します。

 

## <a name="span-idsystemrequirementsspanspan-idsystemrequirementsspanspan-idsystemrequirementsspansystem-requirements"></a><span id="System_Requirements"></span><span id="system_requirements"></span><span id="SYSTEM_REQUIREMENTS"></span>システム要件


イーサネット Nic でカーネルのデバッグには、特定の低レベルのプラットフォームのサポートが必要です。 Windows では、このデバッグ ソリューションに、これらの Nic が PCI または PCIe 経由で接続することが必要です。 ほとんどの場合、単にこれらのサポートされている Nic のいずれかで接続すると、デバッグ エクスペリエンスの堅牢なカーネルできます。 ただし、BIOS 構成の詳細が Windows のデバッグのパスを妨げる場合があります。 次のプラットフォーム要件を考慮する必要があります。

-   システム ファームウェアは、検出し、BIOS 構成されているその他のデバイスとそのリソースが競合しないように、NIC のデバイスを構成する必要があります。

## <a name="span-idfindingthevendoridanddeviceidspanspan-idfindingthevendoridanddeviceidspanspan-idfindingthevendoridanddeviceidspanfinding-the-vendor-id-and-device-id"></a><span id="Finding_the_vendor_ID_and_device_ID"></span><span id="finding_the_vendor_id_and_device_id"></span><span id="FINDING_THE_VENDOR_ID_AND_DEVICE_ID"></span>仕入先 ID とデバイス ID の検索


まずターゲット コンピューターに仕入先 ID およびネットワーク アダプターのデバイス ID を検索します。

-   対象のコンピュータでデバイス マネージャーを開きます (入力**devmgmt**コマンド プロンプト ウィンドウで)。
-   デバイス マネージャーでは、デバッグに使用するネットワーク アダプターを探します。
-   ネットワーク アダプター ノードを右クリックし、選択**プロパティ**します。
-   **詳細**] タブの [**プロパティ**、**ハードウェア Id**。

VEN として、ベンダーとデバイスの Id が表示されます\_*VendorID*と DEV\_*DeviceID*します。 たとえば、PCI を参照してください\\VEN\_8086 & DEV\_104B、仕入先 ID 8086 は、デバイス ID が 104B します。

## <a name="span-idvendorid8086intelcorporationspanspan-idvendorid8086intelcorporationspanspan-idvendorid8086intelcorporationspanvendor-id-8086-intel-corporation"></a><span id="Vendor_ID_8086__Intel_Corporation"></span><span id="vendor_id_8086__intel_corporation"></span><span id="VENDOR_ID_8086__INTEL_CORPORATION"></span>ベンダー ID 8086、Intel Corporation


ベンダー ID 8086、これらのデバイス Id がサポートされています。

0438 043A 043C 0440 1000 1001 1004 1008 1009 100C 100 D 100E 100 F 1010 1011 1012 1013 1014 1015 1016 1017 1018 1019 101A 101 D 101E 1026 1027 1028 1049 104A 104B 104C 104 D 105E 105F 1060 1075 1076 1077 1078 1079 107A 107B 107 C 107 D 107E 107F 108A 108B 108C 1096 1098 1099 109A10A4 10A5 10A7 10A9 10B5 10B9 10BA 10BB 10BC 10BD 10BF 10C 0 10C 2 10C 3 10C 4 10C 5 10C 6 10C 7 10C 8 10C 9 10CB 10CC 10 CD 10CE 10 D 3 10 D 5 10 D 6 10D 9 10DA 10 DB 10DD 10DE 10DF 10E1 10E5 10E6 10E7 10E8 10EA 10EB 10EC 10EF 10F0 10F1 10F4 10F5 10F6 10F7 10F8 10F9 10FA 10FB 10 FC 1501 15021503 1507 150A 150B 150 C 150 D 150E 150F 1510 1511 1514 1516 1517 1518 151C 1521 1522 1523 1524 1525 1526 1527 1528 1529 152A 1533 1534 1535 1536 1537 1538 1539 153A 153B 1546 154A 154D 1557 1558 1559 155A 1560 157B 157 C 1F40 1F41 1F45 294 C
## <a name="span-idvendorid10ecrealteksemiconductorcorpspanspan-idvendorid10ecrealteksemiconductorcorpspanvendor-id-10ec-realtek-semiconductor-corp"></a><span id="vendor_id_10ec__realtek_semiconductor_corp."></span><span id="VENDOR_ID_10EC__REALTEK_SEMICONDUCTOR_CORP."></span>ベンダー ID 10EC、Realtek 半導体 corp.


ベンダー ID 10EC のこれらのデバイス Id がサポートされています。

8136 8137 8167 8168 8169
## <a name="span-idvendorid14e4broadcomspanspan-idvendorid14e4broadcomspanspan-idvendorid14e4broadcomspanvendor-id-14e4-broadcom"></a><span id="Vendor_ID_14E4__Broadcom"></span><span id="vendor_id_14e4__broadcom"></span><span id="VENDOR_ID_14E4__BROADCOM"></span>ベンダー ID 14E4、Broadcom


ベンダー ID 14E4 のこれらのデバイス Id がサポートされています。

1600 1601 1639 163A 163B 163C 1644 1645 1646 1647 1648 164A 164 C 164D 1653 1654 1655 1656 1657 1658 1659 165A 165B 165C 165 D 165E 165F 1668 1669 166A 166B 166 D 166E 1672 1673 1674 1676 1677 1678 1679 167A 167B 167 C 167 D 167F 1680 1681 1684 1688 1690 1691 1692 1693 1694 16961698 1699 169A 169B 169 D 16A0 16A6 16A7 16A8 16AA 16AC 16B0 16B1 16B2 16B4 16B5 16B6 16C 6 16C 7 16DD 16F7 16FD 16FE 16 FF 170 D 170E 170F
## <a name="span-idvendorid1969atheroscommunicationsspanspan-idvendorid1969atheroscommunicationsspanspan-idvendorid1969atheroscommunicationsspanvendor-id-1969-atheros-communications"></a><span id="Vendor_ID_1969__Atheros_Communications"></span><span id="vendor_id_1969__atheros_communications"></span><span id="VENDOR_ID_1969__ATHEROS_COMMUNICATIONS"></span>ベンダー ID 1969 年 Atheros 通信


ベンダー ID 1969、これらのデバイス Id がサポートされています。

1062 1063 1073 1083 1090 1091 10A0 10A1 10B0 10B1 10C0 10C1 10D0 10D1 10E0 10E1 10F0 10F1 2060 2062 E091 E0A1 E0B1 E0C1 E0D1 E0E1 E0F1
## <a name="span-idvendorid19a2serverenginesemulexspanspan-idvendorid19a2serverenginesemulexspanspan-idvendorid19a2serverenginesemulexspanvendor-id-19a2-serverengines-emulex"></a><span id="Vendor_ID_19A2__ServerEngines__Emulex_"></span><span id="vendor_id_19a2__serverengines__emulex_"></span><span id="VENDOR_ID_19A2__SERVERENGINES__EMULEX_"></span>ベンダー ID 19A2、ServerEngines (Emulex)


ベンダー ID 19A2 のこれらのデバイス Id がサポートされています。

0211 0215 0221 0700 0710
## <a name="span-idvendorid10dfemulexcorporationspanspan-idvendorid10dfemulexcorporationspanspan-idvendorid10dfemulexcorporationspanvendor-id-10df-emulex-corporation"></a><span id="Vendor_ID_10DF__Emulex_Corporation"></span><span id="vendor_id_10df__emulex_corporation"></span><span id="VENDOR_ID_10DF__EMULEX_CORPORATION"></span>ベンダー ID 10DF、Emulex Corporation


ベンダー ID 10DF のこれらのデバイス Id がサポートされています。

0720 E220
## <a name="span-idvendorid15b3mellanoxtechnologyspanspan-idvendorid15b3mellanoxtechnologyspanspan-idvendorid15b3mellanoxtechnologyspanvendor-id-15b3-mellanox-technology"></a><span id="Vendor_ID_15B3__Mellanox_Technology"></span><span id="vendor_id_15b3__mellanox_technology"></span><span id="VENDOR_ID_15B3__MELLANOX_TECHNOLOGY"></span>ベンダー ID 15B3、Mellanox テクノロジ


ベンダー ID 15B3 のこれらのデバイス Id がサポートされています。

1000 1001 1002 1003 1004 1005 1006 1007 1008 1009 100A 100B 100C 100D 100E 100F 1010 6340 6341 634A 634B 6354 6368 6369 6372 6732 6733 673C 673D 6746 6750 6751 675A 6764 6765 676E 6778

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック



[デバッグが自動的に KDNET ネットワーク カーネルの設定](setting-up-a-network-debugging-connection-automatically.md)

[Windows 8 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

 

 







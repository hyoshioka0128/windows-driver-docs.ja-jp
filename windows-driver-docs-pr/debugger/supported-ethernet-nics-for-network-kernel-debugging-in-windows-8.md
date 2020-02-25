---
title: Windows 8 でネットワーク カーネルのデバッグ用にサポートされているイーサネット NIC
description: ターゲットコンピューターで Windows 8 が実行されている場合は、イーサネットネットワークケーブルでカーネルデバッグを行うことができます。 ターゲットコンピューターには、サポートされているネットワークインターフェイスカード (NIC) またはネットワークアダプターが必要です。
ms.assetid: 92FEEBAF-9978-4BDE-BB4F-81454D84A7E7
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 07b9e6ec4ba7b12a3cc2681861dd204d290cb88b
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528952"
---
# <a name="supported-ethernet-nics-for-network-kernel-debugging-in-windows-8"></a>Windows 8 でネットワーク カーネルのデバッグ用にサポートされているイーサネット NIC

ターゲットコンピューターで Windows 8 が実行されている場合は、イーサネットネットワークケーブルでカーネルデバッグを行うことができます。 ターゲットコンピューターには、サポートされているネットワークインターフェイスカード (NIC) またはネットワークアダプターが必要です。

カーネルのデバッグ中、デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ中のコンピューターは*ターゲットコンピューター*と呼ばれます。 詳細については、「 [KDNET Network カーネルデバッグの自動](setting-up-a-network-debugging-connection-automatically.md)セットアップ」を参照してください。

ネットワークケーブルでカーネルデバッグを実行するには、対象のコンピューターにサポートされているネットワークアダプターが必要です。 対象のコンピューターで Windows 8 を実行している場合は、ここに記載されているネットワークアダプターがカーネルデバッグでサポートされます。

Windows 8.1 カーネルデバッグ用にサポートされているネットワークアダプターの一覧については、「 [Windows 8.1 でのネットワークカーネルデバッグのサポートされているイーサネット nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)」を参照して**ください  。**

## <a name="span-idsystem_requirementsspanspan-idsystem_requirementsspanspan-idsystem_requirementsspansystem-requirements"></a><span id="System_Requirements"></span><span id="system_requirements"></span><span id="SYSTEM_REQUIREMENTS"></span>システム要件

イーサネット Nic を使用したカーネルデバッグには、特定の低レベルプラットフォームのサポートが必要です。 Windows では、このデバッグソリューションに PCI/PCIe 経由でこれらの Nic が接続されている必要があります。 ほとんどの場合、これらのサポートされている Nic のいずれかを接続するだけで、堅牢なカーネルデバッグエクスペリエンスが実現します。 ただし、BIOS 構成の詳細によって Windows デバッグパスが妨げられる場合があります。 次のプラットフォーム要件のセットを考慮する必要があります。

- システムファームウェアは、NIC デバイスのリソースが、BIOS で構成されている他のデバイスと競合しないように、NIC デバイスを検出して構成する必要があります。
- システムのファームウェアは、プリフェッチ可能とマークされていないアドレスウィンドウに NIC のリソースを配置する必要があります。

## <a name="span-idfinding_the_vendor_id_and_device_idspanspan-idfinding_the_vendor_id_and_device_idspanspan-idfinding_the_vendor_id_and_device_idspanfinding-the-vendor-id-and-device-id"></a><span id="Finding_the_vendor_ID_and_device_ID"></span><span id="finding_the_vendor_id_and_device_id"></span><span id="FINDING_THE_VENDOR_ID_AND_DEVICE_ID"></span>ベンダー ID とデバイス ID の検索

まず、ターゲットコンピューター上のネットワークアダプターのベンダー ID とデバイス ID を検索します。

-  ターゲットコンピューターでデバイスマネージャーを開きます (コマンドプロンプトウィンドウで「 **devmgmt.msc** 」と入力します)。
-  デバイスマネージャーで、デバッグに使用するネットワークアダプターを指定します。
-  ネットワークアダプター ノードを右クリックし、**プロパティ** を選択します。
-  **[詳細]** タブの **[プロパティ]** で、 **[ハードウェア id]** を選択します。

ベンダー Id とデバイス Id は、VEN\_*VendorID*および DEV\_*DeviceID*として表示されます。 たとえば、PCI\\VEN\_8086 & DEV\_104B が表示されている場合、ベンダ ID は8086、デバイス ID は104B です。

## <a name="span-idvendor_id_8086__intel_corporationspanspan-idvendor_id_8086__intel_corporationspanspan-idvendor_id_8086__intel_corporationspanvendor-id-8086-intel-corporation"></a><span id="Vendor_ID_8086__Intel_Corporation"></span><span id="vendor_id_8086__intel_corporation"></span><span id="VENDOR_ID_8086__INTEL_CORPORATION"></span>ベンダー ID 8086、Intel Corporation

ベンダー ID 8086 では、次のデバイス Id がサポートされています。

1000 1001 1004 1008 1009 100C 100C 100C 100C 1010 1011 1012 1013 1014 1015 1016 1017 1018 1019 101A 101A 101A 1026 1027 1028 1049 101A 101A 101A 101A 101A 105F 1060 1075 1076 1077 1078 1079 101A 101A 101A 101A 107E 101A 101A 108B 108C 1096 1098 1099 109A 101A 101A 10A7 10A910B5 10B5 10B5 10B5 10B5 10B5 10B5 10C9 10B5 10B5 10B5 10B5 10D3 10D5 10D6 10D9 10B5 10B5 10B5 10E7 10B5 10B5 10B5 6 1501 1502 1503 150A 150A 150D 150A 150A 1510 1511 1516 1518 1521 1522 1523 1524 1526 294C
## <a name="span-idvendor_id_10ec__realtek_semiconductor_corpspanspan-idvendor_id_10ec__realtek_semiconductor_corpspanvendor-id-10ec-realtek-semiconductor-corp"></a><span id="vendor_id_10ec__realtek_semiconductor_corp."></span><span id="VENDOR_ID_10EC__REALTEK_SEMICONDUCTOR_CORP."></span>ベンダー ID 10EC、Realtek 半導体 Corp。


ベンダー ID 10EC の場合、次のデバイス Id がサポートされます。

8136 8137 8167 8168 8169
## <a name="span-idvendor_id_14e4__broadcomspanspan-idvendor_id_14e4__broadcomspanspan-idvendor_id_14e4__broadcomspanvendor-id-14e4-broadcom"></a><span id="Vendor_ID_14E4__Broadcom"></span><span id="vendor_id_14e4__broadcom"></span><span id="VENDOR_ID_14E4__BROADCOM"></span>仕入先 ID 14E4、Broadcom


ベンダー ID 14E4 の場合、次のデバイス Id がサポートされています。

1600 1601 1639 163A 163A 163A 1644 1645 1646 1647 1648 164A 164A 164A 1653 1654 1655 1656 1657 1658 1659 163A 163A 163A 163A 163A 165F 1668 1669 163A 163A 166D 166E 1672 1673 1674 1676 1677 1678 1679 163A 163A 163A 163A 163A 1680 1681 1684 1688 1690 1691 1692 1693 1694 16961698 1699 169A 169B 169D 16A0 169D 169D 169D 16AA 16AC 16B0 169D 16B2 16B4 16B5 16B6 16C6 169D 16DD 169D 16FD 16FE 16FF 170D 170D 170D
## <a name="span-idvendor_id_1969__atheros_communicationsspanspan-idvendor_id_1969__atheros_communicationsspanspan-idvendor_id_1969__atheros_communicationsspanvendor-id-1969-atheros-communications"></a><span id="Vendor_ID_1969__Atheros_Communications"></span><span id="vendor_id_1969__atheros_communications"></span><span id="VENDOR_ID_1969__ATHEROS_COMMUNICATIONS"></span>ベンダー ID 1969、Atheros Communications


Atheros ネットワークアダプターのサポートは、Qualcomm から入手できる個別のモジュールによって提供されます。 これらのデバイス Id はサポートされています。

1062 1063 1073 1083 1090 1091 10A0 10A1 10B0 10B1 10C0 10C1 10D0 10D1 10E0 10E1 10F0 10F1 2060 2062 E091 E0A1 E0B1 E0C1 E0D1 E0E1 E0F1
## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック



[KDNET Network カーネルデバッグを自動的に設定する](setting-up-a-network-debugging-connection-automatically.md)

[Windows 8.1 でのネットワークカーネルデバッグ用にサポートされるイーサネット Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

[Windows 10 でのネットワークカーネルデバッグ用にサポートされているイーサネット Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)

 

 







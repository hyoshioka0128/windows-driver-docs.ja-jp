---
title: Windows 10 でネットワーク カーネル デバッグ用にサポートされているイーサネット NIC
description: ターゲットコンピューターで Windows を実行している場合は、イーサネットネットワークケーブルでカーネルデバッグを行うことができます。 ターゲットコンピューターには、サポートされているネットワークインターフェイスカード (NIC) またはネットワークアダプターが必要です。
ms.assetid: F98A7ACE-DD04-423C-A438-89E21363C693
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5c412b601acb17ea32b6a9a9b3607583f7520595
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528954"
---
# <a name="supported-ethernet-nics-for-network-kernel-debugging-in-windows-10"></a>Windows 10 でネットワーク カーネル デバッグ用にサポートされているイーサネット NIC

ターゲットコンピューターで Windows を実行している場合は、イーサネットネットワークケーブルでカーネルデバッグを行うことができます。 ターゲットコンピューターには、サポートされているネットワークインターフェイスカード (NIC) またはネットワークアダプターが必要です。

カーネルのデバッグ中、デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ中のコンピューターは*ターゲットコンピューター*と呼ばれます。 詳細については、「 [KDNET Network カーネルデバッグの自動](setting-up-a-network-debugging-connection-automatically.md)セットアップ」を参照してください。

ネットワークケーブルでカーネルデバッグを実行するには、対象のコンピューターにサポートされているネットワークアダプターが必要です。 対象のコンピューターで Windows を実行している場合は、ここに示されているネットワークアダプターがカーネルデバッグでサポートされます。

**バージョン情報**

サポートされているアダプターの一覧は、次のバージョンの Windows 用です。

- Windows 10 バージョン1809
- Windows Server 2019

**以前のリリースの Windows のアダプターサポート**  

Windows の特定のリリースでサポートされている Nic のセットを確認するには、Windows の特定のリリースに付属の WDK によってインストールされた、デバッガーディレクトリ内の `VerifiedNicList.xml` ファイルを調べます。 64ビット Windows の場合、既定では、次のディレクトリにインストールされます。

`C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\VerifiedNicList.xml`

特定のリリースに対して WDK に付属している VerifiedNicList を確認する必要があります。これは、以前のリリースには存在しない Windows の新しいリリースに追加のハードウェアサポートが追加されるためです。  そのため、その特定のリリースの VerifiedNicLIst ファイルを確認する必要があります。

## <a name="span-idfinding_the_vendor_id_and_device_idspanspan-idfinding_the_vendor_id_and_device_idspanspan-idfinding_the_vendor_id_and_device_idspanfinding-the-vendor-id-and-device-id"></a><span id="Finding_the_vendor_ID_and_device_ID"></span><span id="finding_the_vendor_id_and_device_id"></span><span id="FINDING_THE_VENDOR_ID_AND_DEVICE_ID"></span>ベンダー ID とデバイス ID の検索

まず、ターゲットコンピューター上のネットワークアダプターのベンダー ID とデバイス ID を検索します。

-  ターゲットコンピューターでデバイスマネージャーを開きます (コマンドプロンプトウィンドウで「 **devmgmt.msc** 」と入力します)。
-  デバイスマネージャーで、デバッグに使用するネットワークアダプターを指定します。
-  ネットワークアダプター ノードを右クリックし、**プロパティ** を選択します。
-  **[詳細]** タブの **[プロパティ]** で、 **[ハードウェア id]** を選択します。

ベンダー Id とデバイス Id は、VEN\_*VendorID*および DEV\_*DeviceID*として表示されます。 たとえば、PCI\\VEN\_8086 & DEV\_104B が表示されている場合、ベンダ ID は8086、デバイス ID は104B です。

## <a name="span-idvendor_id_8086__intel_corporationspanspan-idvendor_id_8086__intel_corporationspanspan-idvendor_id_8086__intel_corporationspanvendor-id-8086-intel-corporation"></a><span id="Vendor_ID_8086__Intel_Corporation"></span><span id="vendor_id_8086__intel_corporation"></span><span id="VENDOR_ID_8086__INTEL_CORPORATION"></span>ベンダー ID 8086、Intel Corporation


ベンダー ID 8086 では、次のデバイス Id がサポートされています。

0001 0008 000C 000C 0438 043A 043A 0440 0470 1000 1001 1004 1008 1009 100C 100C 100C 100C 1010 1011 1012 1013 1014 1015 1016 1017 1018 1019 101A 101A 101A 1026 1027 1028 1049 101A 101A 101A 101A 101A 105F 1060 1071 1075 1076 1077 1078 1079 101A 101A 101A 101A 107E 101A 101A108B 108C 1096 1098 1099 109A 10A4 10A4 10A7 10A9 10A4 10A4 10A4 10A4 10A4 10A4 10A4 10C0 10A4 10C3 10C4 10C5 10A4 10C7 10C8 10C9 10A4 10A4 10 CD 10A4 10D3 10D5 10D6 10D9 10A4 10A4 10A4 10A4 106E7 10A4 10A4 10A4 10A4 10A4 10A4 10A4 10A4 10F5 10F6 10F7F5 10F6 10F7 10A410F9 10F9 10F9 11A9 1501 1502 1503 1507 150A 150B 150A 150D 150A 150A 1510 1511 1514 1516 1517 1518 150A 1521 1522 1523 1524 1525 1526 1527 1528 1529 150A 1533 1534 1535 1536 1537 1538 1539 150A 150A 1546 150A 150A 1557 1558 1559 150A 1560 1563 156F 1570 150A 150A 150A 150A15A2 15A3 15A2 15A2 15A2 15A2 15A2 15B7 15B8 17D0 1F40 1F40 1F40 1F40 1F72 211B 2159 294C 8976

## <a name="span-idvendor_id_10ec__realtek_semiconductor_corpspanspan-idvendor_id_10ec__realtek_semiconductor_corpspanvendor-id-10ec-realtek-semiconductor-corp"></a><span id="vendor_id_10ec__realtek_semiconductor_corp."></span><span id="VENDOR_ID_10EC__REALTEK_SEMICONDUCTOR_CORP."></span>ベンダー ID 10EC、Realtek 半導体 Corp。


ベンダー ID 10EC の場合、次のデバイス Id がサポートされます。

8136 8137 8166 8167 8168 8169

## <a name="span-idvendor_id_14e4__broadcomspanspan-idvendor_id_14e4__broadcomspanspan-idvendor_id_14e4__broadcomspanvendor-id-14e4-broadcom"></a><span id="Vendor_ID_14E4__Broadcom"></span><span id="vendor_id_14e4__broadcom"></span><span id="VENDOR_ID_14E4__BROADCOM"></span>仕入先 ID 14E4、Broadcom


ベンダー ID 14E4 の場合、次のデバイス Id がサポートされています。

1600 1601 1639 163A 163A 163A 163A 163A 1641 1642 1643 1644 1645 1646 1647 1648 164A 164A 164A 164A 164A 1650 1653 1654 1655 1656 1657 1659 163A 163A 163A 163A 163A 165F 1662 1663 1665 1668 1669 163A 163A 166D 166E 1672 1673 1674 1676 1677 1678 1679 163A 163A 163A 163A168A 168D 168E 1680 1681 1682 1683 1684 1686 1687 1688 1690 1691 1692 1693 1694 1696 1698 1699 169A 169B 169D 16 A0 168A 168A 168A 168A 16A6 16A7 16A8 168A 168A 168A 168A 16B1 16B2 16B3 168A 16C7 168A 16B7 168A 168A 168A 170D 170D 170D

## <a name="span-idvendor_id_1969__atheros_communicationsspanspan-idvendor_id_1969__atheros_communicationsspanspan-idvendor_id_1969__atheros_communicationsspanvendor-id-1969-atheros-communications"></a><span id="Vendor_ID_1969__Atheros_Communications"></span><span id="vendor_id_1969__atheros_communications"></span><span id="VENDOR_ID_1969__ATHEROS_COMMUNICATIONS"></span>ベンダー ID 1969、Atheros Communications


ベンダー ID 1969 では、次のデバイス Id がサポートされています。

1062 1063 1073 1083 1090 1091 10A0 10A1 10B0 10B1 10C0 10C1 10D0 10D1 10E0 10E1 10F0 10F1 2060 2062 E091 E0A1 E0B1 E0C1 E0D1 E0E1 E0F1

## <a name="span-idvendor_id_19a2__serverengines__emulex_spanspan-idvendor_id_19a2__serverengines__emulex_spanspan-idvendor_id_19a2__serverengines__emulex_spanvendor-id-19a2-serverengines-emulex"></a><span id="Vendor_ID_19A2__ServerEngines__Emulex_"></span><span id="vendor_id_19a2__serverengines__emulex_"></span><span id="VENDOR_ID_19A2__SERVERENGINES__EMULEX_"></span>ベンダー ID 19A2、ServerEngines (Emulex)


ベンダ ID 19A2 の場合、次のデバイス Id がサポートされます。

0211 0215 0221 0700 0710

## <a name="span-idvendor_id_10df__emulex_corporationspanspan-idvendor_id_10df__emulex_corporationspanspan-idvendor_id_10df__emulex_corporationspanvendor-id-10df-emulex-corporation"></a><span id="Vendor_ID_10DF__Emulex_Corporation"></span><span id="vendor_id_10df__emulex_corporation"></span><span id="VENDOR_ID_10DF__EMULEX_CORPORATION"></span>ベンダ ID 10DF、Emulex Corporation


ベンダー ID 10DF では、これらのデバイス Id がサポートされています。

0720 E220

## <a name="span-idvendor_id_15b3__mellanox_technologyspanspan-idvendor_id_15b3__mellanox_technologyspanspan-idvendor_id_15b3__mellanox_technologyspanvendor-id-15b3-mellanox-technology"></a><span id="Vendor_ID_15B3__Mellanox_Technology"></span><span id="vendor_id_15b3__mellanox_technology"></span><span id="VENDOR_ID_15B3__MELLANOX_TECHNOLOGY"></span>ベンダー ID 15B3、Mellanox テクノロジ


ベンダー ID 15B3 の場合、次のデバイス Id がサポートされます。

1000 1001 1002 1003 1004 1005 1006 1007 1008 1009 100A 100B 100B 100B 100B 100B 1010 1013 1015 1017 1019 101B 101D 101D 1021 1023 1025 1027 1029/673C 6340 6341 634A 634A 6354 6368 6369 6372 6732 6733 3C 673C 6746 6750 6751 634A 6764 6765 634A 6778

## <a name="span-idvendor_id_1137__cisco_systems_incspanspan-idvendor_id_1137__cisco_systems_incspanspan-idvendor_id_1137__cisco_systems_incspanvendor-id-1137-cisco-systems-inc"></a><span id="Vendor_ID_1137__Cisco_Systems_Inc"></span><span id="vendor_id_1137__cisco_systems_inc"></span><span id="VENDOR_ID_1137__CISCO_SYSTEMS_INC"></span>ベンダ ID 1137、Cisco Systems Inc.


ベンダー ID 1137 では、次のデバイス Id がサポートされています。

0043

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのネットワークケーブル経由でのカーネルモードデバッグの設定](setting-up-a-network-debugging-connection-in-visual-studio.md)

[KDNET Network カーネルデバッグを自動的に設定する](setting-up-a-network-debugging-connection-automatically.md)

[KDNET Network カーネルデバッグの手動設定](setting-up-a-network-debugging-connection.md)

[Windows 8 でのネットワークカーネルデバッグ用にサポートされているイーサネット Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

[Windows 8.1 でのネットワークカーネルデバッグ用にサポートされるイーサネット Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

 

 







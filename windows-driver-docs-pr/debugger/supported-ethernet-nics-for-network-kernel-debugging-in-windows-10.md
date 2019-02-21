---
title: Windows 10 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート
description: ターゲット コンピューターで Windows を実行している場合に、イーサネット ネットワーク ケーブル経由でカーネル デバッグを行うことができます。 対象のコンピュータは、サポートされているネットワーク インターフェイス カード (NIC) またはネットワーク アダプターが必要です。
ms.assetid: F98A7ACE-DD04-423C-A438-89E21363C693
ms.date: 12/04/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4653c71d6a736abf7f36a2d713384d0d6478666e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548800"
---
# <a name="supported-ethernet-nics-for-network-kernel-debugging-in-windows-10"></a>Windows 10 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート

ターゲット コンピューターで Windows を実行している場合に、イーサネット ネットワーク ケーブル経由でカーネル デバッグを行うことができます。 対象のコンピュータは、サポートされているネットワーク インターフェイス カード (NIC) またはネットワーク アダプターが必要です。

カーネルのデバッグ中には、デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコンピューターを呼び出すと、*ターゲット コンピューター*します。 行う[ネットワーク ケーブル経由でのカーネル デバッグ](setting-up-a-network-debugging-connection.md)、ターゲット コンピューターがサポートされているネットワーク アダプターをいる必要があります。 ターゲット コンピューターには、Windows が実行されているが、ここで記載されているネットワーク アダプターは、カーネルのデバッグ サポートされます。

**バージョン情報**  

サポートされているアダプターの一覧は、次のバージョンの Windows

-   Windows 10、バージョンは 1809
-   Windows Server 2019


**Windows の以前のリリースのアダプターのサポート**  

Nic のセットは、特定のリリースの Windows のサポートを確認するのには、確認、`VerifiedNicList.xml`その特定のリリースの Windows に同梱されている WDK でインストールされているデバッガー ディレクトリ内にあるファイル。 既定では、64 ビットの Windows では、このディレクトリにインストールされます。

`C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\VerifiedNicList.xml`

以前のリリースでは Windows の新しいリリースに追加のハードウェア サポートが追加されるため、特定のリリースの WDK で出荷される VerifiedNicList.xml を確認するが必要です。  このため、その特定のリリースの VerifiedNicLIst.xml ファイルを確認する必要があります。


## <a name="span-idfindingthevendoridanddeviceidspanspan-idfindingthevendoridanddeviceidspanspan-idfindingthevendoridanddeviceidspanfinding-the-vendor-id-and-device-id"></a><span id="Finding_the_vendor_ID_and_device_ID"></span><span id="finding_the_vendor_id_and_device_id"></span><span id="FINDING_THE_VENDOR_ID_AND_DEVICE_ID"></span>仕入先 ID とデバイス ID の検索

まずターゲット コンピューターに仕入先 ID およびネットワーク アダプターのデバイス ID を検索します。

-   対象のコンピュータでデバイス マネージャーを開きます (入力**devmgmt**コマンド プロンプト ウィンドウで)。
-   デバイス マネージャーでは、デバッグに使用するネットワーク アダプターを探します。
-   ネットワーク アダプター ノードを右クリックし、選択**プロパティ**します。
-   **詳細**] タブの [**プロパティ**、**ハードウェア Id**。

VEN として、ベンダーとデバイスの Id が表示されます\_*VendorID*と DEV\_*DeviceID*します。 たとえば、PCI を参照してください\\VEN\_8086 & DEV\_104B、仕入先 ID 8086 は、デバイス ID が 104B します。

## <a name="span-idvendorid8086intelcorporationspanspan-idvendorid8086intelcorporationspanspan-idvendorid8086intelcorporationspanvendor-id-8086-intel-corporation"></a><span id="Vendor_ID_8086__Intel_Corporation"></span><span id="vendor_id_8086__intel_corporation"></span><span id="VENDOR_ID_8086__INTEL_CORPORATION"></span>ベンダー ID 8086、Intel Corporation


ベンダー ID 8086、これらのデバイス Id がサポートされています。

0001 0008 000 C 000 D 0438 043A 043C 0440 0470 1000 1001 1004 1008 1009 100C 100 D 100E 100 F 1010 1011 1012 1013 1014 1015 1016 1017 1018 1019 101A 101 D 101E 1026 1027 1028 1049 104A 104B 104C 104 D 105E 105F 1060 1071 1075 1076 1077 1078 1079 107A 107B 107 C 107 D 107E 107F 108A108B 108C 1096 1098 1099 109A 10A4 10A5 10A7 10A9 10B5 10B9 10BA 10BB 10BC 10BD 10BF 10C 0 10C 2 10C 3 10C 4 10C 5 10C 6 10C 7 10C 8 10C 9 10CB 10CC 10 CD 10CE 10 D 3 10 D 5 10 D 6 10D 9 10DA 10 DB 10DD 10DE 10DF 10E1 10E5 10E6 10E7 10E8 10EA 10EB 10EC 10EF 10F0 10F1 10F4 10F5 10F6 10F7 10F810F9 10FB 10 FC 11A9 1501 1502 1503 1507 150A 150B 150 C 150 D 150E 150F 1510 1511 1514 1516 1517 1518 151C 1521 1522 1523 1524 1525 1526 1527 1528 1529 152A 1533 1534 1535 1536 1537 1538 1539 153A 153B 1546 154A 154D 1557 1558 1559 155A 1560 1563 156F 1570 157B 157 C 15A0 15A115A2 15A3 15AA 15AB 15AC 15AD 15AE 15B7 15B8 17 D 0 1F40 1F41 1F45 1F63 1F72 211B 2159 294 C 8976

## <a name="span-idvendorid10ecrealteksemiconductorcorpspanspan-idvendorid10ecrealteksemiconductorcorpspanvendor-id-10ec-realtek-semiconductor-corp"></a><span id="vendor_id_10ec__realtek_semiconductor_corp."></span><span id="VENDOR_ID_10EC__REALTEK_SEMICONDUCTOR_CORP."></span>ベンダー ID 10EC、Realtek 半導体 corp.


ベンダー ID 10EC のこれらのデバイス Id がサポートされています。

8136 8137 8166 8167 8168 8169

## <a name="span-idvendorid14e4broadcomspanspan-idvendorid14e4broadcomspanspan-idvendorid14e4broadcomspanvendor-id-14e4-broadcom"></a><span id="Vendor_ID_14E4__Broadcom"></span><span id="vendor_id_14e4__broadcom"></span><span id="VENDOR_ID_14E4__BROADCOM"></span>ベンダー ID 14E4、Broadcom


ベンダー ID 14E4 のこれらのデバイス Id がサポートされています。

1600 1601 1639 163A 163B 163C 163D 163E 1641 1642 1643 1644 1645 1646 1647 1648 164A 164C 164 D 164 E 164F 1650 1653 1654 1655 1656 1657 1659 165A 165B 165C 165 D 165E 165F 1662 1663 1665 1668 1669 166A 166B 166 D 166E 1672 1673 1674 1676 1677 1678 1679 167A 167B 167 C 167 D 167F168A 168 D 168E 1680 1681 1682 1683 1684 1686 1687 1688 1690 1691 1692 1693 1694 1696 1698 1699 169A 169B 169 D 16A0 16A1 16A2 16A4 16A5 16A6 16A7 16A8 16AA 16AC 16AE 16B0 16B1 16B2 16B3 16B4 16B5 16B6 16B7 16C 6 16C 7 16DD 16F7 16FD 16FE 16 FF 170 D 170E 170F

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

1000 1001 1002 1003 1004 1005 1006 1007 1008 1009 100 A 力 +100 100 C 100 D 100E 100 F 1010 1013 1015 1017 1019 101B 101 D 101F 1021 1023 1025 1027 1029 102B 102F 6340 6341 634A 634B 6354 6368 6369 6372 6732 6733 673C 673D 6746 6750 6751 675A 6764 6765 676E 6778

## <a name="span-idvendorid1137ciscosystemsincspanspan-idvendorid1137ciscosystemsincspanspan-idvendorid1137ciscosystemsincspanvendor-id-1137-cisco-systems-inc"></a><span id="Vendor_ID_1137__Cisco_Systems_Inc"></span><span id="vendor_id_1137__cisco_systems_inc"></span><span id="VENDOR_ID_1137__CISCO_SYSTEMS_INC"></span>1137、Cisco Systems Inc のベンダー ID


ベンダー ID 1137、これらのデバイス Id がサポートされています。

0043

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Visual Studio でのネットワーク ケーブル経由でのカーネル モードのデバッグのセットアップ](setting-up-a-network-debugging-connection-in-visual-studio.md)

[デバッグが自動的に KDNET ネットワーク カーネルの設定](setting-up-a-network-debugging-connection-automatically.md)

[KDNET のネットワーク カーネル デバッグを手動での設定](setting-up-a-network-debugging-connection.md)

[Windows 8 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

[Windows 8.1 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

 

 







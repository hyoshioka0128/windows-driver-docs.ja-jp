---
title: Windows 10 でネットワーク カーネル デバッグ用にサポートされているイーサネット NIC
description: ターゲットコンピューターで Windows を実行している場合は、イーサネットネットワークケーブルでカーネルデバッグを行うことができます。 ターゲットコンピューターには、サポートされているネットワークインターフェイスカード (NIC) またはネットワークアダプターが必要です。
ms.assetid: F98A7ACE-DD04-423C-A438-89E21363C693
ms.date: 06/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: 49cee589c33b008aae631ae853ea9ac30b6339c6
ms.sourcegitcommit: 0e83928aac8f171980e94b67f9291468e6e68093
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2020
ms.locfileid: "84336391"
---
# <a name="supported-ethernet-nics-for-network-kernel-debugging-in-windows-10"></a>Windows 10 でネットワーク カーネル デバッグ用にサポートされているイーサネット NIC

ターゲットコンピューターで Windows を実行している場合は、イーサネットネットワークケーブルでカーネルデバッグを行うことができます。 ターゲットコンピューターには、サポートされているネットワークインターフェイスカード (NIC) またはネットワークアダプターが必要です。

カーネルのデバッグ中、デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ中のコンピューターは*ターゲットコンピューター*と呼ばれます。 詳細については、「 [KDNET Network カーネルデバッグの自動](setting-up-a-network-debugging-connection-automatically.md)セットアップ」を参照してください。

ネットワークケーブルでカーネルデバッグを実行するには、対象のコンピューターにサポートされているネットワークアダプターが必要です。 対象のコンピューターで Windows を実行している場合は、ここに示されているネットワークアダプターがカーネルデバッグでサポートされます。

**バージョン情報**

サポートされているアダプターの一覧は、次のバージョンの Windows 用です。

- Windows 10 バージョン 2004
- Windows Server 2019

**以前のリリースの Windows のアダプターサポート**  

Windows の特定のリリースでサポートされている Nic のセットを確認するには、 `VerifiedNicList.xml` その特定のリリースの windows に付属している WDK によってインストールされた、デバッガーのディレクトリにあるファイルを調べます。 64ビット Windows の場合、既定では、次のディレクトリにインストールされます。

`C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\VerifiedNicList.xml`

特定のリリースに対して WDK に付属している VerifiedNicList を確認する必要があります。これは、以前のリリースには存在しない Windows の新しいリリースに追加のハードウェアサポートが追加されるためです。  そのため、その特定のリリースの VerifiedNicLIst ファイルを確認する必要があります。

## <a name="finding-the-vendor-id-and-device-id"></a>ベンダー ID とデバイス ID の検索

ターゲットコンピューター上のネットワークアダプターのベンダー ID とデバイス ID を検索します。

- ターゲットコンピューターでデバイスマネージャーを開きます (コマンドプロンプトウィンドウで「 **devmgmt.msc** 」と入力します)。
- デバイスマネージャーで、デバッグに使用するネットワークアダプターを指定します。
- [ネットワークアダプター] ノードを右クリックし、[**プロパティ**] を選択します。
- [**詳細**] タブの [**プロパティ**] で、[**ハードウェア id**] を選択します。

ベンダー Id とデバイス Id は、VEN \_ *VENDORID*と DEV DeviceID として表示され \_ *DeviceID*ます。 たとえば、PCI \\ VEN \_ 8086&DEV 104b と表示されている場合、 \_ ベンダ id は8086で、デバイス ID は104b です。

## <a name="vendor-id-8086-intel-corporation"></a>ベンダー ID 8086、Intel Corporation

ベンダー ID 8086 では、次のデバイス Id がサポートされています。

0001 0008 000C 000C 0438 043A 043A 0440 0470 1000 1001 1004 1008 1009 100C 100C 100C 100C 1010 1011 1012 1013 1014 1015 1016 1017 1018 1019 101A 101A 101A 1026 1027 1028 1049 101A 101A 101A 101A 101A 105F 1060 1071 1075 1076 1077 1078 1079 101A 101A 101A 101A 107E 101A 101A 108B 108C 1096 1098 1099 109A 101A 101A 10A7 10A9 101A 101A 101A 101A 101A 101A 101A 10C0 101A 10C3 10C4 10C5 101A 10C7 10C810C9 10CB 10CC 10 CD 10CE 10C9 10D5 10C9 10C9 10DA 10DB 10DD 10-10DF 10C9 10E5 10E6 10C9 10E8 10EA 10EB 10EC 10EF 10F0 10F1 10F4 10C9 10C9 10C9 10F8 10F9 10FB 10FC 11A9 1501 1502 1503 1507 150A 150B 150A 150D 150A 150A 1510 1511 1514 1516 1517 1518 150A 1521 1522 1523 1524 1525 1526 1527 1528 1529 150A 1533 1534 1535 1536 1537 1538 1539 150A 150A 1546 150A 150A 1557 1558 1559 150A 1560 1563 156F1570 157B 157B 157B 157B 157B 15A3 157B 157B 157B 157B 157B 15B7 15B8 157B 157B 157B 157B 157B 15DD 6 15D7 15D8 157B 157B 15E1 157B 15E3 17D0 1F40 1F40 1F40 1F40 1F72 211B 2159 294C 8976

## <a name="vendor-id-10ec-realtek-semiconductor-corp"></a>ベンダー ID 10EC、Realtek 半導体 Corp。

ベンダー ID 10EC の場合、次のデバイス Id がサポートされます。

2502 2600 3000 8125 8136 8137 8161 8166 8167 8168 8169 8225

## <a name="vendor-id-14e4-broadcom"></a>仕入先 ID 14E4、Broadcom

ベンダー ID 14E4 の場合、次のデバイス Id がサポートされています。

1600 1601 1639 163A 163A 163A 163A 163A 1641 1642 1643 1644 1645 1646 1647 1648 164A 164A 164A 164A 164A 1650 1653 1654 1655 1656 1657 1659 163A 163A 163A 163A 163A 165F 1662 1663 1665 1668 1669 163A 163A 166D 166E 1672 1673 1674 1676 1677 1678 1679 163A 163A 163A 163A 163A 163A 168D 168E 1680 1681 1682 1683 1684 1686 1687 1688 1690 1691 1692 1693 1694 1696 1698 1699 169A 169B 169D 163A 163A 163A16A4 16A4 16A6 16A7 16A8 16A4 16A4 16A4 16A4 16B1 16B2 16B3 16A4 16A4 16A4 16B7 16A4 16C7 16A4 16F7 16A4 16A4 16A4 170D 170D 170D

## <a name="vendor-id-1969-atheros-communications"></a>ベンダー ID 1969、Atheros Communications

ベンダー ID 1969 では、次のデバイス Id がサポートされています。

1062 1063 1073 1083 1090 1091 10A0 10A0 10A0 10B1 10C0 10A0 10A0 10D1 10A0 10E1 10A0 10A0 2060 2062 E091 E0A1 E0B1 E0C1 E0D1 E0E1 E0F1

## <a name="vendor-id-19a2-serverengines-emulex"></a>ベンダー ID 19A2、ServerEngines (Emulex)

ベンダ ID 19A2 の場合、次のデバイス Id がサポートされます。

0211 0215 0221 0700 0710

## <a name="vendor-id-10df-emulex-corporation"></a>ベンダ ID 10DF、Emulex Corporation

ベンダー ID 10DF では、これらのデバイス Id がサポートされています。

0720 E220

## <a name="vendor-id-15b3-mellanox-technology"></a>ベンダー ID 15B3、Mellanox テクノロジ

ベンダー ID 15B3 の場合、次のデバイス Id がサポートされます。

1000 1001 1002 1003 1004 1005 1006 1007 1008 1009 100A 100B 100B 100B 100B 100B 1010 1013 1015 1017 1019 101B 101D 101D 1021 1023 1025 1027 1029/673C 6340 6341 634A 634A 6354 6368 6369 6372 6732 6733 3C 673C 6746 6750 6751 634A 6764 6765 634A 6778

## <a name="vendor-id-1137-cisco-systems-inc"></a>ベンダ ID 1137、Cisco Systems Inc.

ベンダー ID 1137 では、次のデバイス Id がサポートされています。

0043

## <a name="related-topics"></a>関連トピック

[Visual Studio でのネットワーク ケーブル経由でのカーネルモード デバッグの設定](setting-up-a-network-debugging-connection-in-visual-studio.md)

[KDNET ネットワーク カーネル デバッグの自動設定](setting-up-a-network-debugging-connection-automatically.md)

[KDNET ネットワーク カーネル デバッグの手動設定](setting-up-a-network-debugging-connection.md)

[Windows 8 でネットワーク カーネルのデバッグ用にサポートされているイーサネット NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8.md)

[Windows 8.1 でネットワーク カーネル デバッグ用にサポートされているイーサネット NIC](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)

 

 







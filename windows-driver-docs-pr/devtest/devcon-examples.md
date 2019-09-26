---
title: デバイス コンソール (DevCon.exe) の例
description: デバイス コンソール (DevCon.exe) の例
ms.assetid: 5af1e777-04ba-4e83-b239-f568a02a9460
keywords:
- DevCon WDK、例
- デバイスコンソール WDK、例
- WDK DevCon の例
- DevCon WDK、コマンド
- デバイスコンソール WDK、コマンド
- コマンド WDK DevCon
- 例 44 HAL を強制的に更新する
- HAL の更新の例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c96013d8cc2ec547a687ece45189caba95771e97
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284926"
---
# <a name="device-console-devconexe-examples"></a>デバイス コンソール (DevCon.exe) の例


## <span id="ddk_devcon_examples_tools"></span><span id="DDK_DEVCON_EXAMPLES_TOOLS"></span>


ここでは、次のデバイスコンソール (DevCon) コマンドの例を紹介します。

### <a name="span-iddevcon_hwidsspanspan-iddevcon_hwidsspandevcon-hwids"></a><span id="devcon_hwids"></span><span id="DEVCON_HWIDS"></span>DevCon HwIDs

[例 1:すべてのハードウェア Id を検索する](#ddk_example_1_find_all_hardware_ids_tools)

[例 2:パターンを使用してハードウェア Id を検索する](#ddk_example_2_find_hardware_ids_by_using_a_pattern_tools)

[例 3:クラスを使用してハードウェア Id を検索する](#ddk_example_3_find_hardware_ids_by_using_a_class_tools)

### <a name="span-iddevcon_classesspanspan-iddevcon_classesspandevcon-classes"></a><span id="devcon_classes"></span><span id="DEVCON_CLASSES"></span>DevCon クラス

[例 4:ローカルコンピューター上のクラスを一覧表示する](#ddk_example_4_list_classes_on_the_local_computer_tools)

[例 5:リモートコンピューター上のクラスを一覧表示する](#ddk_example_5_list_classes_on_the_remote_computer_tools)

### <a name="span-iddevcon_listclassspanspan-iddevcon_listclassspandevcon-listclass"></a><span id="devcon_listclass"></span><span id="DEVCON_LISTCLASS"></span>DevCon ListClass

[例 6:デバイスセットアップクラスでのデバイスの一覧表示](#ddk_example_6_list_the_devices_in_a_device_setup_class_tools)

[例 7:リモートコンピューター上の複数のクラスのデバイスを一覧表示する](#ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute)

### <a name="span-iddevcon_driverfilesspanspan-iddevcon_driverfilesspandevcon-driverfiles"></a><span id="devcon_driverfiles"></span><span id="DEVCON_DRIVERFILES"></span>DevCon DriverFiles

[例 8:すべてのドライバーファイルを一覧表示する](#ddk_example_8_list_all_driver_files_tools)

[例 9:特定のデバイスのドライバーファイルを一覧表示する](#ddk_example_9_list_the_driver_files_of_a_particular_device_tools)

### <a name="span-iddevcon_drivernodesspanspan-iddevcon_drivernodesspandevcon-drivernodes"></a><span id="devcon_drivernodes"></span><span id="DEVCON_DRIVERNODES"></span>DevCon DriverNodes

[例 10:ハードウェア ID パターン別のドライバーパッケージの一覧表示](#ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools)

[例 11:デバイスインスタンス ID パターン別のドライバーパッケージの一覧表示](#ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool)

### <a name="span-iddevcon_resourcesspanspan-iddevcon_resourcesspandevcon-resources"></a><span id="devcon_resources"></span><span id="DEVCON_RESOURCES"></span>DevCon リソース

[例 12:デバイスのクラスのリソースを一覧表示する](#ddk_example_12_list_resources_of_a_class_of_devices_tools)

[例 13:リモートコンピューター上のデバイスのリソースを ID で一覧表示する](#ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too)

### <a name="span-iddevcon_stackspanspan-iddevcon_stackspandevcon-stack"></a><span id="devcon_stack"></span><span id="DEVCON_STACK"></span>DevCon スタック

[例 14:記憶装置のドライバースタックを表示する](#ddk_example_14_display_the_driver_stack_for_storage_devices_tools)

[例 15:デバイスのセットアップクラスを検索する](#ddk_example_15_find_the_setup_class_of_a_device_tools)

[例 16:リモートコンピューター上の関連するデバイスのスタックを表示する](#ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu)

### <a name="span-iddevcon_statusspanspan-iddevcon_statusspandevcon-status"></a><span id="devcon_status"></span><span id="DEVCON_STATUS"></span>DevCon ステータス

[例 17:ローカルコンピューター上のすべてのデバイスの状態を表示する](#ddk_example_17_display_the_status_of_all_devices_on_the_local_computer)

[例 18:デバイスインスタンス ID 別にデバイスの状態を表示する](#ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to)

[例 19:リモートコンピューター上の関連するデバイスの状態を表示する](#ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu)

### <a name="span-iddevcon_findspanspan-iddevcon_findspandevcon-find"></a><span id="devcon_find"></span><span id="DEVCON_FIND"></span>DevCon 検索

[例 20:ハードウェア ID パターン別のデバイスの検索](#ddk_example_20_find_devices_by_hardware_id_pattern_tools)

[例 21:デバイスインスタンス ID またはクラス別のデバイスの検索](#ddk_example_21_find_devices_by_device_instance_id_or_class_tools)

### <a name="span-iddevcon_findallspanspan-iddevcon_findallspandevcon-findall"></a><span id="devcon_findall"></span><span id="DEVCON_FINDALL"></span>DevCon FindAll

[例 22:セットアップクラスでのすべてのデバイスの検索 (および検索)](#ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools)

### <a name="span-iddevcon_classfilterspanspan-iddevcon_classfilterspandevcon-classfilter"></a><span id="devcon_classfilter"></span><span id="DEVCON_CLASSFILTER"></span>DevCon ClassFilter

[例 23:セットアップクラスのフィルタードライバーを表示する](#ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools)

[例 24:セットアップクラスへのフィルタードライバーの追加](#ddk_example_24_add_a_filter_driver_to_a_setup_class_tools)

[例 25:クラスの一覧にフィルタードライバーを挿入する](#ddk_example_25_insert_a_filter_driver_in_the_class_list_tools)

[例 26:フィルタードライバーの置換](#ddk_example_26_replace_a_filter_driver_tools)

[例 27:フィルタードライバーの順序を変更する](#ddk_example_27_change_the_order_of_filter_drivers_tools)

### <a name="span-iddevcon_enablespanspan-iddevcon_enablespandevcon-enable"></a><span id="devcon_enable"></span><span id="DEVCON_ENABLE"></span>DevCon 有効化

[例 28:特定のデバイスを有効にする](#ddk_example_28_enable_a_particular_device_tools)

[例 29:クラス別にデバイスを有効にする](#ddk_example_29_enable_devices_by_class_tools)

### <a name="span-iddevcon_disablespanspan-iddevcon_disablespandevcon-disable"></a><span id="devcon_disable"></span><span id="DEVCON_DISABLE"></span>DevCon の無効化

[例 30:ID パターンでデバイスを無効にする](#ddk_example_30_disable_devices_by_an_id_pattern_tools)

[例 31:デバイスインスタンス ID でデバイスを無効にする](#ddk_example_31_disable_devices_by_device_instance_id_tools)

### <a name="span-iddevcon_update_and_updatenispanspan-iddevcon_update_and_updatenispandevcon-update-and-updateni"></a><span id="devcon_update_and_updateni"></span><span id="DEVCON_UPDATE_AND_UPDATENI"></span>DevCon Update と UpdateNI

[例 32:通信ポートのドライバーを更新する](#ddk_example_32_update_the_driver_for_communication_ports_tools)

[例 44:HAL を強制的に更新する](#ddk_example_44_forcibly_update_the_hal_tools)

### <a name="span-iddevcon_installspanspan-iddevcon_installspandevcon-install"></a><span id="devcon_install"></span><span id="DEVCON_INSTALL"></span>DevCon インストール

[例 33:デバイスをインストールする](#ddk_example_33_install_a_device_tools)

[例 34:無人セットアップを使用してデバイスをインストールする](#ddk_example_34_install_a_device_using_unattended_setup_tools)

### <a name="span-iddevcon_removespanspan-iddevcon_removespandevcon-remove"></a><span id="devcon_remove"></span><span id="DEVCON_REMOVE"></span>DevCon の削除

[例 35:デバイスインスタンス ID パターン別にデバイスを削除する](#ddk_example_35_remove_devices_by_device_instance_id_pattern_tools)

[例 36:特定のネットワークデバイスを削除する](#ddk_example_36_remove_a_particular_network_device_tools)

### <a name="span-iddevcon_rescanspanspan-iddevcon_rescanspandevcon-rescan"></a><span id="devcon_rescan"></span><span id="DEVCON_RESCAN"></span>DevCon 再スキャン

[例 37:新しいデバイスのコンピューターをスキャンする](#ddk_example_37_scan_the_computer_for_new_devices_tools)

### <a name="span-iddevcon_restartspanspan-iddevcon_restartspandevcon-restart"></a><span id="devcon_restart"></span><span id="DEVCON_RESTART"></span>DevCon の再起動

[例 38:デバイスを再起動する](#ddk_example_38_restart_a_device_tools)

### <a name="span-iddevcon_status2spanspan-iddevcon_status2spandevcon-status"></a><span id="devcon_status2"></span><span id="DEVCON_STATUS2"></span>DevCon ステータス

[例 39:ローカルコンピューターを再起動する](#ddk_example_39_reboot_the_local_computer_tools)

### <a name="span-iddevcon_sethwidspanspan-iddevcon_sethwidspandevcon-sethwid"></a><span id="devcon_sethwid"></span><span id="DEVCON_SETHWID"></span>DevCon SetHwID

[例 40:レガシデバイスにハードウェア ID を割り当てる](#ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools)

[例 41:リモートコンピューター上のすべてのレガシデバイスにハードウェア ID を追加する](#ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com)

[例 42:リモートコンピューター上のすべてのレガシデバイスからハードウェア ID を削除する](#ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot)

[例 43:ハードウェア Id の追加、削除、交換](#ddk_example_43_add_delete_and_replace_hardwareids_tools)

[例 44:HAL を強制的に更新する](#ddk_example_44_forcibly_update_the_hal_tools)

### <a name="span-iddevcon_dp_add__dp_deleted__dp_enumspanspan-iddevcon_dp_add__dp_deleted__dp_enumspandevcon-dp_add-dp_deleted-dp_enum"></a><span id="devcon_dp_add__dp_deleted__dp_enum"></span><span id="DEVCON_DP_ADD__DP_DELETED__DP_ENUM"></span>DevCon dp\_add、dp\_deleted、dp\_enum

[例 45:ドライバーパッケージの追加と削除](example-45--add-and-remove-driver-packages.md)

### <span id="ddk_example_1_find_all_hardware_ids_tools"></span><span id="DDK_EXAMPLE_1_FIND_ALL_HARDWARE_IDS_TOOLS"></span><a name="ddk_example_1_find_all_hardware_ids_tools"></a>例 1:すべてのハードウェア Id を検索する

DevCon 操作では Id と ID パターンを使用してデバイスを識別するため、DevCon を使用する際の一般的な最初の手順は、コンピューター上のデバイス用のハードウェア ID 参照ファイルを作成することです。

次のコマンドでは、Id とデバイスの説明を返す、 [**DevCon HwIDs**](devcon-hwids.md)操作が使用されています。 ワイルドカード文字 ( **\*** ) を使用して、ローカルコンピューター上のすべてのデバイスを表します。

```
devcon hwids *
```

出力の時間が長く、繰り返し使用されるため、出力をテキストファイルに保存して参照します。

次のコマンドは、ワイルドカード文字 **\*** () を使用して、コンピューター上のすべてのデバイスを表します。 リダイレクト文字 ( *<em>&gt;</em>* ) を使用して、コマンドの出力を hwids ファイルに保存します。

```
devcon hwids * > hwids.txt
```

次のコマンドは、リモートコンピューター上のデバイスのハードウェア Id Server01 を検索します。 **/M**パラメーターを使用して、リモートコンピューターの名前を指定します。 このコマンドは、後で参照する\_ために、出力を server01 hwids ファイルにリダイレクトします。

**注:**   ユーザーがリモートコンピューターに対して必要なアクセス許可を持っていない場合、このコマンドは失敗します。 リモートコンピューターで DevCon コマンドを実行するには、グループポリシー設定で、プラグアンドプレイサービスをリモートコンピューターで実行できるようにする必要があります。 Windows Vista および Windows 7 を実行しているコンピューターでは、グループポリシーによって、サービスへのリモートアクセスが既定で無効になります。 Windows Driver Kit (WDK) 8.1 および Windows Driver Kit (WDK) 8 を実行するコンピューターでは、リモートアクセスは使用できません。

 

```
devcon /m:\\server01 hwids * > server01_hwids.txt
```

### <span id="ddk_example_2_find_hardware_ids_by_using_a_pattern_tools"></span><span id="DDK_EXAMPLE_2_FIND_HARDWARE_IDS_BY_USING_A_PATTERN_TOOLS"></span><a name="ddk_example_2_find_hardware_ids_by_using_a_pattern_tools"></a>例 2:パターンを使用してハードウェア Id を検索する

特定のデバイスのハードウェア Id を検索するには、ハードウェア ID またはパターン、互換性のある ID またはパターン、デバイスインスタンス ID またはパターン、またはデバイスセットアップクラスの名前を入力します。

次のコマンドは、 **DevCon HwIDs**操作とパターンを使用して、コンピューター上のフロッピーディスクドライブのハードウェア id を検索します。 (ユーザーは、デバイス識別子のいずれかにパターンが表示されていることを前提としています)。このコマンドでは、ワイルドカード **\*** 文字 () を使用して、任意の id で "フロッピー" という単語の前または後にあるすべての文字を表します。

```
devcon hwids *floppy*
```

応答として、コンピューター上のフロッピーディスクドライブのデバイスインスタンス ID、ハードウェア ID、および互換性のある ID が表示されます。 これらの Id は、以降の DevCon コマンドで使用できます。

```
FDC\GENERIC_FLOPPY_DRIVE\5&39194F6D&0&0
    Name: Floppy disk drive
    Hardware ID's:
        FDC\GENERIC_FLOPPY_DRIVE
    Compatible ID's:
        GenFloppyDisk
1 matching device(s) found.
```

この場合、"フロッピー" という語句は、コンピューター上の1つのデバイスのハードウェア ID または互換性のある ID で発生します。 複数のデバイスの ID で発生した場合は、Id に "フロッピー" が付いたすべてのデバイスが出力に表示されます。

### <span id="ddk_example_3_find_hardware_ids_by_using_a_class_tools"></span><span id="DDK_EXAMPLE_3_FIND_HARDWARE_IDS_BY_USING_A_CLASS_TOOLS"></span><a name="ddk_example_3_find_hardware_ids_by_using_a_class_tools"></a>例 3:クラスを使用してハードウェア Id を検索する

次のコマンドでは、 [**DevCon HwIDs**](devcon-hwids.md)操作とデバイスセットアップクラスを使用して、Ports デバイスセットアップクラスのすべてのデバイスのハードウェア id を検索します。 クラス名の前 **=** の等号 () は、ID ではなくクラスであることを示します。

```
devcon hwids =ports
```

応答として、[ポートのセットアップ] クラスには、3つのデバイスのハードウェア Id と互換性 Id が表示されます。

```
ACPI\PNP0401\4&B4063F4&0
    Name: ECP Printer Port (LPT1)
    Hardware ID's:
        ACPI\PNP0401
        *PNP0401
ACPI\PNP0501\1
    Name: Communications Port (COM1)
    Hardware ID's:
        ACPI\PNP0501
        *PNP0501
ACPI\PNP0501\2
    Name: Communications Port (COM2)
    Hardware ID's:
        ACPI\PNP0501
        *PNP0501
3 matching device(s) found.
```

### <span id="ddk_example_4_list_classes_on_the_local_computer_tools"></span><span id="DDK_EXAMPLE_4_LIST_CLASSES_ON_THE_LOCAL_COMPUTER_TOOLS"></span><a name="ddk_example_4_list_classes_on_the_local_computer_tools"></a>例 4:ローカルコンピューター上のクラスを一覧表示する

DevCon 操作ではデバイスのセットアップクラスを使用してデバイスを識別できるため、コンピューター上のデバイスのセットアップクラスであるデバイスの参照ファイルを作成すると便利です。

次のコマンドは、コンピューター上のすべてのクラスのリストと説明を返す、 [**DevCon クラス**](devcon-classes.md)操作を使用します。

```
devcon classes
```

出力の時間が長く、繰り返し使用されるため、出力をテキストファイルに保存して参照します。

次のコマンドは、コンピューター上のすべてのデバイスクラスを表示します。 リダイレクト文字 ( **&gt;** ) を使用して、コマンドの出力を classes ファイルに保存します。

```
devcon classes > classes.txt
```

### <span id="ddk_example_5_list_classes_on_the_remote_computer_tools"></span><span id="DDK_EXAMPLE_5_LIST_CLASSES_ON_THE_REMOTE_COMPUTER_TOOLS"></span><a name="ddk_example_5_list_classes_on_the_remote_computer_tools"></a>例 5:リモートコンピューター上のクラスを一覧表示する

次のコマンドは、 [**DevCon クラス**](devcon-classes.md)操作を使用して、リモートコンピューター上のデバイスセットアップクラス Server01 を一覧表示します。

```
devcon /m:\\server01 classes
```

出力の時間が長く、繰り返し使用されるため、出力をテキストファイルに保存して参照します。

次のコマンドは、リダイレクト文字 ( **&gt;** ) を使用して、コマンドの出力\_を server01 ファイルに保存します。

```
devcon /m:\\server01 classes > server01_classes.txt
```

### <span id="ddk_example_6_list_the_devices_in_a_device_setup_class_tools"></span><span id="DDK_EXAMPLE_6_LIST_THE_DEVICES_IN_A_DEVICE_SETUP_CLASS_TOOLS"></span><a name="ddk_example_6_list_the_devices_in_a_device_setup_class_tools"></a>例 6:デバイスセットアップクラスでのデバイスの一覧表示

次のコマンドは、 [**DevCon listclass**](devcon-listclass.md)操作を使用して、ネットワークアダプターのデバイスセットアップクラスである Net 内のデバイスを一覧表示します。

```
devcon listclass net
```

応答で、デバイスインスタンス ID と、Net setup クラスの各デバイスの説明が表示されます。

```
Listing 6 device(s) for setup class "Net" (Network adapters).
PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028&REV_78\4&BB7B4AE&0&60F0: 3Com 3C920 Integrated Fast Ethernet Controller (3C905C-TX Compatible)
ROOT\MS_L2TPMINIPORT\0000                                   : WAN Miniport (L2TP)
ROOT\MS_NDISWANIP\0000                                      : WAN Miniport (IP)
ROOT\MS_PPPOEMINIPORT\0000                                  : WAN Miniport (PPPOE)
ROOT\MS_PPTPMINIPORT\0000                                   : WAN Miniport (PPTP)
ROOT\MS_PTIMINIPORT\0000                                    : Direct Parallel
```

この表示は興味深いものですが、Net setup クラスのデバイスのハードウェア Id は提供されません。 次のコマンドは、 [**DevCon HwIDs**](devcon-hwids.md)操作を使用して、Net setup クラスのデバイスを一覧表示します。 **DevCon HwIDs**コマンドでは、クラス名の前に等号 ( **=** ) が付いており、ID ではなくクラスであることを示しています。

```
devcon hwids =net
```

結果の表示には、Net クラスに含まれるデバイスの一覧が表示されます。この表示には、デバイスのインスタンス ID、ハードウェア Id、および互換性のあるデバイスの Id がクラスに含まれています。

```
PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028&REV_78\4&BB7B4AE&0&60F0
    Name: 3Com 3C920 Integrated Fast Ethernet Controller (3C905C-TX Compatible)
    Hardware ID's:
        PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028&REV_78
        PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028
        PCI\VEN_10B7&DEV_9200&CC_020000
        PCI\VEN_10B7&DEV_9200&CC_0200
    Compatible ID's:
        PCI\VEN_10B7&DEV_9200&REV_78
        PCI\VEN_10B7&DEV_9200
        PCI\VEN_10B7&CC_020000
        PCI\VEN_10B7&CC_0200
 PCI\VEN_10B7
        PCI\CC_020000
 PCI\CC_0200
ROOT\MS_L2TPMINIPORT\0000
    Name: WAN Miniport (L2TP)
    Hardware ID's:
        ms_l2tpminiport
ROOT\MS_NDISWANIP\0000
    Name: WAN Miniport (IP)
    Hardware ID's:
        ms_ndiswanip
ROOT\MS_PPPOEMINIPORT\0000
    Name: WAN Miniport (PPPOE)
    Hardware ID's:
        ms_pppoeminiport
ROOT\MS_PPTPMINIPORT\0000
    Name: WAN Miniport (PPTP)
    Hardware ID's:
        ms_pptpminiport
ROOT\MS_PTIMINIPORT\0000
    Name: Direct Parallel
    Hardware ID's:
        ms_ptiminiport
6 matching device(s) found.
```

### <span id="ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute"></span><span id="DDK_EXAMPLE_7_LIST_THE_DEVICES_IN_MULTIPLE_CLASSES_ON_A_REMOTE_COMPUTE"></span><a name="ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute"></a>例 7:リモートコンピューター上の複数のクラスのデバイスを一覧表示する

次のコマンドは、 [**DevCon ListClass**](devcon-listclass.md)操作を使用して、リモートコンピューターである Server01 上の DISKDRIVE、CDROM、およびテープドライブクラスのデバイスを一覧表示します。

```
devcon /m:\\server01 listclass diskdrive cdrom tapedrive
```

応答として、[DevCon] は、リモートコンピューター上のこれらのクラスのデバイスを表示します。

```
Listing 1 device(s) for setup class "DiskDrive" (Disk drives) on \\server01.
IDE\DISKWDC_WD204BA_____________________________16.13M16\4457572D414D3730323136333938203120202020: WDC WD204BA
Listing 1 device(s) for setup class "CDROM" (DVD/CD-ROM drives) on \\server01.
IDE\CDROMSAMSUNG_DVD-ROM_SD-608__________________2.2_____\4&13B4AFD&0&0.0.0: SAMSUNG DVD-ROM SD-608
No devices for setup class "TapeDrive" (Tape drives) on \\server01.
```

### <span id="ddk_example_8_list_all_driver_files_tools"></span><span id="DDK_EXAMPLE_8_LIST_ALL_DRIVER_FILES_TOOLS"></span><a name="ddk_example_8_list_all_driver_files_tools"></a>例 8:すべてのドライバーファイルを一覧表示する

次のコマンドは、 [**DevCon DriverFiles**](devcon-driverfiles.md)操作を使用して、システム上のデバイスが使用するドライバーのファイル名を一覧表示します。 このコマンドは、ワイルドカード文字 **\*** () を使用して、システム上のすべてのデバイスを示します。 出力は広いため、コマンドはリダイレクト文字 ( *<em>&gt;</em>* ) を使用して、出力を参照ファイル driverfiles にリダイレクトします。

```
devcon driverfiles * > driverfiles.txt
```

### <span id="ddk_example_9_list_the_driver_files_of_a_particular_device_tools"></span><span id="DDK_EXAMPLE_9_LIST_THE_DRIVER_FILES_OF_A_PARTICULAR_DEVICE_TOOLS"></span><a name="ddk_example_9_list_the_driver_files_of_a_particular_device_tools"></a>例 9:特定のデバイスのドライバーファイルを一覧表示する

次のコマンドは、 [**DevCon DriverFiles**](devcon-driverfiles.md)操作を使用して、ローカルコンピューター上のマウスデバイスが使用するデバイスドライバーを検索します。 デバイスは、そのハードウェア id の1つである HID\\Vid\_045e & Pid\_0039 & Rev\_0121 によって識別されます。 ハードウェア ID は、アンパサンド文字 ( **&** ) が含まれているため、引用符で囲まれています。

```
devcon driverfiles "HID\Vid_045e&Pid_0039&Rev_0121"
```

応答として、[DevCon] には、マウスデバイスをサポートする2つのデバイスドライバーが表示されます。

```
HID\VID_045E&PID_0039\6&DC36FDE&0&0000
    Name: Microsoft USB IntelliMouse Optical
    Driver installed from c:\windows\inf\msmouse.inf [HID_Mouse_Inst]. 2 file(s)
 used by driver:
        C:\WINDOWS\System32\DRIVERS\mouhid.sys
        C:\WINDOWS\System32\DRIVERS\mouclass.sys
1 matching device(s) found.
```

### <span id="ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools"></span><span id="DDK_EXAMPLE_10_LIST_DRIVER_PACKAGES_BY_HARDWARE_ID_PATTERN_TOOLS"></span><a name="ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools"></a>例 10:ハードウェア ID パターン別のドライバーパッケージの一覧表示

次のコマンドは、 [**DevCon DriverNodes**](devcon-drivernodes.md)コマンドと ID パターンを使用して、ソフトウェアで列挙されたデバイスのドライバーノードを一覧表示します。 パターンは、同じセットアップクラスに含まれていない可能性がある類似のデバイスに関する情報を見つけるのに役立ちます。

次のコマンドは、ID パターン**sw\\** * を使用して、ハードウェア id または互換性のある id が "sw" で始まるデバイス、つまりソフトウェアで列挙されたデバイスを指定します。

```
devcon drivernodes sw*
```

応答として、ソフトウェアで列挙されたデバイスのドライバーノードがシステムに表示されます。

```
SW\{A7C7A5B0-5AF3-11D1-9CED-00A024BF0407}\{9B365890-165F-11D0-A195-0020AFD156E4}

 Name: Microsoft Kernel System Audio Device
DriverNode #0:
    Inf file is c:\windows\inf\wdmaudio.inf
    Inf section is WDM_SYSAUDIO
    Driver description is Microsoft Kernel System Audio Device
    Manufacturer name is Microsoft
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002244
        Inf is digitally signed
SW\{B7EAFDC0-A680-11D0-96D8-00AA0051E51D}\{9B365890-165F-11D0-A195-0020AFD156E4}

    Name: Microsoft Kernel Wave Audio Mixer
DriverNode #0:
    Inf file is c:\windows\inf\wdmaudio.inf
    Inf section is WDM_KMIXER
    Driver description is Microsoft Kernel Wave Audio Mixer
    Manufacturer name is Microsoft
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002244
        Inf is digitally signed
SW\{CD171DE3-69E5-11D2-B56D-0000F8754380}\{9B365890-165F-11D0-A195-0020AFD156E4}

    Name: Microsoft WINMM WDM Audio Compatibility Driver
DriverNode #0:
    Inf file is c:\windows\inf\wdmaudio.inf
    Inf section is WDM_WDMAUD
    Driver description is Microsoft WINMM WDM Audio Compatibility Driver
    Manufacturer name is Microsoft
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002244
        Inf is digitally signed
3 matching device(s) found.
```

### <span id="ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool"></span><span id="DDK_EXAMPLE_11_LIST_DRIVER_PACKAGES_BY_DEVICE_INSTANCE_ID_PATTERN_TOOL"></span><a name="ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool"></a>例 11:デバイスインスタンス ID パターン別のドライバーパッケージの一覧表示

次のコマンドは、 [**DevCon drivernodes**](devcon-drivernodes.md)操作を使用して、デバイスインスタンス id がルート\\メディアで始まるすべてのデバイス (つまり、列挙\\ルート\\メディアレジストリサブキー内のデバイス) のドライバーパッケージを一覧表示します. このコマンドは、アット文字 ( **@** ) を使用して、その語句がデバイスインスタンス ID に含まれていることを示します。

```
devcon drivernodes @ROOT\MEDIA*
```

応答として、デバイスインスタンス ID が "ルート\\メディア" で始まるデバイスのドライバーノードが表示されます。

```
ROOT\MEDIA\MS_MMACM
    Name: Audio Codecs
DriverNode #0:
    Inf file is c:\windows\inf\wave.inf
    Inf section is MS_MMACM
    Driver description is Audio Codecs
    Manufacturer name is (Standard system devices)
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002240
        Inf is digitally signed
ROOT\MEDIA\MS_MMDRV
    Name: Legacy Audio Drivers
DriverNode #0:
    Inf file is c:\windows\inf\wave.inf
    Inf section is MS_MMDRV
    Driver description is Legacy Audio Drivers
    Manufacturer name is (Standard system devices)
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002240
        Inf is digitally signed
ROOT\MEDIA\MS_MMMCI
    Name: Media Control Devices
DriverNode #0:
    Inf file is c:\windows\inf\wave.inf
    Inf section is MS_MMMCI
    Driver description is Media Control Devices
    Manufacturer name is (Standard system devices)
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002240
        Inf is digitally signed
ROOT\MEDIA\MS_MMVCD
    Name: Legacy Video Capture Devices
DriverNode #0:
    Inf file is c:\windows\inf\wave.inf
    Inf section is MS_MMVCD
    Driver description is Legacy Video Capture Devices
    Manufacturer name is (Standard system devices)
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002240
        Inf is digitally signed
ROOT\MEDIA\MS_MMVID
    Name: Video Codecs
DriverNode #0:
    Inf file is c:\windows\inf\wave.inf
    Inf section is MS_MMVID
    Driver description is Video Codecs
    Manufacturer name is (Standard system devices)
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002240
        Inf is digitally signed
5 matching device(s) found.
```

### <span id="ddk_example_12_list_resources_of_a_class_of_devices_tools"></span><span id="DDK_EXAMPLE_12_LIST_RESOURCES_OF_A_CLASS_OF_DEVICES_TOOLS"></span><a name="ddk_example_12_list_resources_of_a_class_of_devices_tools"></a>例 12:デバイスのクラスのリソースを一覧表示する

次のコマンドは、 [**DevCon resources**](devcon-resources.md)操作を使用して、Hdc デバイスセットアップクラスのデバイスに割り当てられたリソースを表示します。 このクラスには、IDE コントローラーが含まれています。 等号 ( **=** ) は、ID ではなくクラスであることを示すために "hdc" の前に付加されます。

```
devcon resources =hdc
```

応答として、ローカルコンピューター上の IDE コントローラーに割り当てられているリソースが表示されます。

```
PCI\VEN_8086&DEV_244B&SUBSYS_00000000&REV_02\3&29E81982&0&F9
    Name: Intel(r) 82801BA Bus Master IDE Controller
    Device is currently using the following resources:
        IO  : ffa0-ffaf
PCIIDE\IDECHANNEL\4&37E53584&0&0
    Name: Primary IDE Channel
    Device is currently using the following resources:
        IO  : 01f0-01f7
        IO  : 03f6-03f6
        IRQ : 14
PCIIDE\IDECHANNEL\4&37E53584&0&1
    Name: Secondary IDE Channel
    Device is currently using the following resources:
        IO  : 0170-0177
        IO  : 0376-0376
        IRQ : 15
3 matching device(s) found.
```

### <span id="ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too"></span><span id="DDK_EXAMPLE_13_LIST_RESOURCES_OF_DEVICE_ON_A_REMOTE_COMPUTER_BY_ID_TOO"></span><a name="ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too"></a>例 13:リモートコンピューター上のデバイスのリソースを ID で一覧表示する

次のコマンドでは、 [**DevCon resources**](devcon-resources.md)操作を使用して、リモートコンピューター Server01 上のシステムタイマーに割り当てられているリソースを一覧表示します。 このコマンドは、システムタイマーのハードウェア ID である ACPI\\PNP0100 を使用して、デバイスを指定します。

```
devcon /m:\\Server01 resources *PNP0100
```

応答として、Server01 システムタイマーのリソースが表示されます。

```
ROOT\*PNP0100\PNPBIOS_8
    Name: System timer
    Device has the following resources reserved:
        IO  : 0040-005f
        IRQ : 0
1 matching device(s) found on \\server01.
```

次のコマンドでは、DevCon resources コマンドでリモートシステムタイマーのデバイスインスタンス ID を使用します。 アット文字 ( **@** ) は、その文字列がハードウェア id や互換性のある id ではなく、デバイスインスタンス ID であることを示します。

```
devcon /m:\\Server01 resources @ACPI\PNP0100\4&b4063f4&0
```

### <span id="ddk_example_14_display_the_driver_stack_for_storage_devices_tools"></span><span id="DDK_EXAMPLE_14_DISPLAY_THE_DRIVER_STACK_FOR_STORAGE_DEVICES_TOOLS"></span><a name="ddk_example_14_display_the_driver_stack_for_storage_devices_tools"></a>例 14:記憶装置のドライバースタックを表示する

次のコマンドは、 [**DevCon Stack**](devcon-stack.md)操作を使用して Volume setup クラスのデバイスを検索し、それらのデバイスに予想されるドライバースタックを表示します。 等号 ( **=** ) は、文字列がクラス名であることを示します。

```
devcon stack =Volume
```

応答として、[DevCon] には、ボリュームクラスのデバイスに予想されるスタックが表示されます。 返されるデータには、デバイスインスタンス ID と各デバイスの説明、デバイスセットアップクラスの GUID と名前、上位および下位のフィルタードライバーの名前、およびサービス (存在する場合) の制御が含まれます。

```
STORAGE\VOLUME\1&30A96598&0&SIGNATURE32323533OFFSET271167600LENGTH6E00D0C00
    Name: Generic volume
    Setup Class: {71A27CDD-812A-11D0-BEC7-08002BE2092F} Volume
    Class upper filters:
        VolSnap
    Controlling service:
        (none)
STORAGE\VOLUME\1&30A96598&0&SIGNATURE32323533OFFSET7E00LENGTH27115F800
    Name: Generic volume
    Setup Class: {71A27CDD-812A-11D0-BEC7-08002BE2092F} Volume
    Class upper filters:
        VolSnap
    Controlling service:
        (none)
2 matching device(s) found.
```

### <span id="ddk_example_15_find_the_setup_class_of_a_device_tools"></span><span id="DDK_EXAMPLE_15_FIND_THE_SETUP_CLASS_OF_A_DEVICE_TOOLS"></span><a name="ddk_example_15_find_the_setup_class_of_a_device_tools"></a>例 15:デバイスのセットアップクラスを検索する

[**DevCon Stack**](devcon-stack.md)操作は、上位および下位のフィルタードライバーに加えて、デバイスのセットアップクラスを返します。 次のコマンドは、デバイスインスタンス ID を検索し、デバイスインスタンス ID を使用してそのセットアップクラスを検索することによって、プリンタポートインターフェイスのセットアップクラスを検索します。

次のコマンドは、 [**DevCon HwIDs**](devcon-hwids.md)操作を使用して、プリンターポートインターフェイスのデバイスインスタンス ID を検索します。プリンターポートのハードウェア id に "LPT" という語句を使用します。

```
devcon hwids *lpt*
```

応答として、DevCon はデバイスインスタンス ID (太字で表示) とプリンターポートインターフェイスのハードウェア ID を返します。

```
LPTENUM\MICROSOFTRAWPORT\5&CA97D7E&0&LPT1
    Name: Printer Port Logical Interface
    Hardware ID's:
        LPTENUM\MicrosoftRawPort958A
        MicrosoftRawPort958A
1 matching device(s) found.
```

次のコマンドは、 [**DevCon Stack**](devcon-stack.md)操作を使用して、デバイスインスタンス ID によって表されるデバイスのデバイスセットアップクラスを検索します。 At 文字 ( **@** ) は、デバイスインスタンス id として id を識別します。 ID はアンパサンド文字を含むため、引用符で囲まれています。

```
devcon stack "@LPTENUM\MICROSOFTRAWPORT\5&CA97D7E&0&LPT1"
```

応答として、[DevCon] には、クラスを含むプリンタポートインターフェイスのドライバースタックが表示されます。 プリンターポートがシステムクラスにあることが表示されます。

```
LPTENUM\MICROSOFTRAWPORT\5&CA97D7E&0&LPT1
    Name: Printer Port Logical Interface
    Setup Class: {4D36E97D-E325-11CE-BFC1-08002BE10318} System
    Controlling service:
        (none)
1 matching device(s) found.
```

### <span id="ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu"></span><span id="DDK_EXAMPLE_16_DISPLAY_THE_STACK_FOR_RELATED_DEVICES_ON_A_REMOTE_COMPU"></span><a name="ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu"></a>例 16:リモートコンピューター上の関連するデバイスのスタックを表示する

次のコマンドは、 **DevCon stack**操作を使用して、リモートコンピューター Server01 上のミニポートドライバーデバイスに予想されるスタックを表示します。 このクラスは、ハードウェア ID または互換性 ID に "ミニポート" を含む Net setup クラスのデバイスを検索します。

このコマンドはまず、検索を Net setup クラスに限定し、次に "ミニポート" 文字列を検索します。 Net setup クラス以外のデバイスは検出されません。

```
devcon /m:\\server01 stack =net *miniport*
```

応答として、Server01 上のミニポートドライバーに必要なスタックが表示されます。

```
ROOT\MS_L2TPMINIPORT\0000
    Name: WAN Miniport (L2TP)
    Setup Class: {4D36E972-E325-11CE-BFC1-08002BE10318} Net
    Controlling service:
        Rasl2tp
ROOT\MS_PPPOEMINIPORT\0000
    Name: WAN Miniport (PPPOE)
    Setup Class: {4D36E972-E325-11CE-BFC1-08002BE10318} Net
    Controlling service:
        RasPppoe
    Lower filters:
        NdisTapi
ROOT\MS_PPTPMINIPORT\0000
    Name: WAN Miniport (PPTP)
    Setup Class: {4D36E972-E325-11CE-BFC1-08002BE10318} Net
    Controlling service:
        PptpMiniport
    Lower filters:
        NdisTapi
ROOT\MS_PTIMINIPORT\0000
    Name: Direct Parallel
    Setup Class: {4D36E972-E325-11CE-BFC1-08002BE10318} Net
    Controlling service:
        Raspti
    Lower filters:
        PtiLink
4 matching device(s) found on \\Server01.
```

### <span id="ddk_example_17_display_the_status_of_all_devices_on_the_local_computer"></span><span id="DDK_EXAMPLE_17_DISPLAY_THE_STATUS_OF_ALL_DEVICES_ON_THE_LOCAL_COMPUTER"></span><a name="ddk_example_17_display_the_status_of_all_devices_on_the_local_computer"></a>例 17:ローカルコンピューター上のすべてのデバイスの状態を表示する

次のコマンドでは、 [**DevCon status**](devcon-status.md)操作を使用して、ローカルコンピューター上のすべてのデバイスの状態を検索します。 その後、ログ記録または後で確認するために、状態を .txt ファイルに保存します。 このコマンドは、ワイルドカード文字 **\*** () を使用してすべてのデバイスを *<em>&gt;</em>* 表し、リダイレクト文字 () を使用して、出力を test.txt ファイルにリダイレクトします。

```
devcon status * > status.txt
```

### <span id="ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to"></span><span id="DDK_EXAMPLE_18_DISPLAY_THE_STATUS_OF_A_DEVICE_BY_DEVICE_INSTANCE_ID_TO"></span><a name="ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to"></a>例 18:デバイスインスタンス ID 別にデバイスの状態を表示する

特定のデバイスの状態を確認する最も信頼性の高い方法は、デバイスのデバイスインスタンス ID を使用することです。

次のコマンドは、ローカルコンピューター上の i/o コントローラーのデバイスインスタンス ID を[**DevCon Status**](devcon-status.md)コマンドで使用します。 このコマンドには、デバイスのデバイスインスタンス ID、PCI\\VEN\_8086 & DEV\_1130 & SUBSYS\_00000000 & REV\_02\\3 & 29e81982 & 0 & 00 が含まれています。 ID のプレフィックスが **@** 付いたアット文字 () は、デバイスインスタンス ID として文字列を識別します。 ID はアンパサンド文字を含むため、引用符で囲む必要があります。

```
devcon status "@PCI\VEN_8086&DEV_1130&SUBSYS_00000000&REV_02\3&29E81982&0&00"
```

応答として、[DevCon] に i/o コントローラーの状態が表示されます。

```
PCI\VEN_8086&DEV_1130&SUBSYS_00000000&REV_02\3&29E81982&0&00
    Name: Intel(R) 82815 Processor to I/O Controller - 1130
    Driver is running.
1 matching device(s) found.
```

### <span id="ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu"></span><span id="DDK_EXAMPLE_19_DISPLAY_THE_STATUS_OF_RELATED_DEVICES_ON_A_REMOTE_COMPU"></span><a name="ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu"></a>例 19:リモートコンピューター上の関連するデバイスの状態を表示する

次のコマンドでは、 [**DevCon status**](devcon-status.md)操作を使用して、リモートコンピューター Server01 上の特定の記憶域に関連するデバイスの状態を表示します。 次のデバイスが検索されます。

-   ディスクドライブ、GenDisk

-   CD-ROM ドライブ、GenCdRom

-   フロッピーディスクドライブ、FDC\\GENERIC\_フロッピー\_ドライブ

-   ボリューム、記憶域\\ボリューム

-   論理ディスクマネージャー、ルート\\DMIO

-   ボリュームマネージャー、ルート\\の FTDISK

-   フロッピーディスクコントローラー、ACPI\\PNP0700

コマンドでは、各 ID はスペースで区切られます。 GenDisk と GenCdRom は互換性のある Id であるのに対し、他の Id はハードウェア Id です。

```
devcon /m:\\server01 status GenDisk GenCdRom FDC\GENERIC_FLOPPY_DRIVE STORAGE\Volume ROOT\DMIO ROOT\FTDISK ACPI\PNP0700
```

応答で、各デバイスの状態が表示されます。

```
FDC\GENERIC_FLOPPY_DRIVE\1&3A2146F1&0&0
    Name: Floppy disk drive
    Driver is running.
IDE\CDROMSAMSUNG_DVD-ROM_SD-608__________________2.2_____\4&13B4AFD&0&0.0.0
    Name: SAMSUNG DVD-ROM SD-608
    Driver is running.
IDE\DISKWDC_WD204BA_____________________________16.13M16\4457572D414D373032313633393820312
0202020
    Name: WDC WD204BA
    Driver is running.
ROOT\DMIO\0000
    Name: Logical Disk Manager
    Driver is running.
ROOT\FLOPPYDISK\0000
    Device has a problem: 28.
ROOT\FLOPPYDISK\0002
    Device has a problem: 01.
ROOT\FLOPPYDISK\0003
    Device has a problem: 01.
ROOT\FLOPPYDISK\0004
    Device is currently stopped.
ROOT\FTDISK\0000
    Name: Volume Manager
    Driver is running.
STORAGE\VOLUME\1&30A96598&0&SIGNATUREEA1AA9C7OFFSET1770DF800LENGTH3494AEA00
    Name: Generic volume
    Driver is running.
STORAGE\VOLUME\1&30A96598&0&SIGNATUREEA1AA9C7OFFSET7E00LENGTH1770CFC00
    Name: Generic volume
    Driver is running.
11 matching device(s) found on \\Server01.
```

### <span id="ddk_example_20_find_devices_by_hardware_id_pattern_tools"></span><span id="DDK_EXAMPLE_20_FIND_DEVICES_BY_HARDWARE_ID_PATTERN_TOOLS"></span><a name="ddk_example_20_find_devices_by_hardware_id_pattern_tools"></a>例 20:ハードウェア ID パターン別のデバイスの検索

次のコマンドでは、 [**DevCon Find**](devcon-find.md)操作を使用して、リモートコンピューター Server01 上のマウスデバイスを検索します。 具体的には、Server01 コンピューターで、ハードウェア ID または互換性のある ID に "mou" が含まれているデバイスを検索します。

```
devcon /m:\\Server01 find *mou*
```

この場合、DevCon は2つのマウスデバイスの両方を検出しました。

```
ROOT\*PNP0F03\1_0_21_0_31_0                                 : Microsoft PS/2 Mouse
ROOT\RDP_MOU\0000                                           : Terminal Server Mouse Driver
```

すべての DevCon 表示操作でもハードウェア Id が検出されるため、任意のディスプレイ操作を使用してハードウェア Id を検索できます。 出力に必要なコンテンツに基づいて操作を選択します。 たとえば、ローカルコンピューター上のマウス関連デバイスで使用されているデバイスドライバーを検索するには、次のコマンドを送信します。

```
devcon driverfiles *mou*
```

応答として、DevCon によってデバイスが検索され、ドライバーが一覧表示されます。

```
HID\VID_045E&PID_0039\6&DC36FDE&0&0000
    Name: Microsoft USB IntelliMouse Optical
    Driver installed from c:\windows\inf\msmouse.inf [HID_Mouse_Inst]. 2 file(s) used by d
river:
        C:\WINDOWS\System32\DRIVERS\mouhid.sys
        C:\WINDOWS\System32\DRIVERS\mouclass.sys
ROOT\RDP_MOU\0000
    Name: Terminal Server Mouse Driver
    Driver installed from c:\windows\inf\machine.inf [RDP_MOU]. 2 file(s) used by driver:
        C:\WINDOWS\System32\DRIVERS\termdd.sys
        C:\WINDOWS\System32\DRIVERS\mouclass.sys
2 matching device(s) found.
```

### <span id="ddk_example_21_find_devices_by_device_instance_id_or_class_tools"></span><span id="DDK_EXAMPLE_21_FIND_DEVICES_BY_DEVICE_INSTANCE_ID_OR_CLASS_TOOLS"></span><a name="ddk_example_21_find_devices_by_device_instance_id_or_class_tools"></a>例 21:デバイスインスタンス ID またはクラス別のデバイスの検索

次のコマンドは、 [**DevCon Find**](devcon-find.md)操作を使用して、ローカルコンピューター上のすべてのレガシデバイスを表示します。 レガシデバイスはハードウェア ID を持っていないため、デバイスインスタンス id (レジストリパス)、ルート\\レガシ、またはそのセットアップクラスである LegacyDriver を使用して検索する必要があります。

最初のコマンドは、デバイスインスタンス ID パターンを使ってレガシドライバーを検索します。 ID パターンは、デバイスインスタンス ID を示し、 **@** その後にワイルドカード文字 ( **\*** ) を指定して、ルート\\のレガシサブキー内のすべてのデバイスを検索するために、先頭の文字 () で始まります。

```
devcon find @root\legacy*
```

2番目のコマンドは、LegacyDriver クラス内のすべてのデバイスを検索して、レガシデバイスを検索します。

```
devcon find =legacydriver
```

どちらのコマンドも同じ出力を生成します。この場合は、同じ27個のレガシデバイスが検索されます。

```
ROOT\LEGACY_AFD\0000                                        : AFD Networking Support Environment
ROOT\LEGACY_BEEP\0000                                       : Beep
ROOT\LEGACY_DMBOOT\0000                                     : dmboot
ROOT\LEGACY_DMLOAD\0000                                     : dmload
ROOT\LEGACY_FIPS\0000                                       : Fips
ROOT\LEGACY_GPC\0000                                        : Generic Packet Classifier
ROOT\LEGACY_IPSEC\0000                                      : ipsec
ROOT\LEGACY_KSECDD\0000                                     : ksecdd
ROOT\LEGACY_MNMDD\0000                                      : mnmdd
ROOT\LEGACY_MOUNTMGR\0000                                   : mountmgr
ROOT\LEGACY_NDIS\0000                                       : ndis
ROOT\LEGACY_NDISTAPI\0000                                   : Remote Access NDIS TAPI Driver
ROOT\LEGACY_NDISUIO\0000                                    : NDIS Usermode I/O Protocol
ROOT\LEGACY_NDPROXY\0000                                    : NDProxy
ROOT\LEGACY_NETBT\0000                                      : netbt
ROOT\LEGACY_NULL\0000                                       : Null
ROOT\LEGACY_PARTMGR\0000                                    : PartMgr
ROOT\LEGACY_PARVDM\0000                                     : ParVdm
ROOT\LEGACY_RASACD\0000                                     : Remote Access Auto Connection Driver
ROOT\LEGACY_RDPCDD\0000                                     : RDPCDD
ROOT\LEGACY_RDPWD\0000                                      : RDPWD
ROOT\LEGACY_TCPIP\0000                                      : tcpip
ROOT\LEGACY_TDPIPE\0000                                     : TDPIPE
ROOT\LEGACY_TDTCP\0000                                      : TDTCP
ROOT\LEGACY_VGASAVE\0000                                    : VgaSave
ROOT\LEGACY_VOLSNAP\0000                                    : VolSnap
ROOT\LEGACY_WANARP\0000                                     : Remote Access IP ARP Driver
27 matching device(s) found.
```

### <span id="ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools"></span><span id="DDK_EXAMPLE_22_FIND_AND_FIND_ALL_DEVICES_IN_A_SETUP_CLASS_TOOLS"></span><a name="ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools"></a>例 22:セットアップクラスでのすべてのデバイスの検索 (および検索)

次のコマンドは、 [**DevCon FindAll**](devcon-findall.md)操作を使用して、コンピューター上のすべてのデバイスを Net setup クラスで検索します。 等号 ( **=** ) は、Net が ID ではなくセットアップクラスであることを示します。

```
devcon findall =net
```

応答として、[DevCon] には、Net setup クラスに次の7つのデバイスが一覧表示されます。 最初の6つは標準のミニポートドライバーデバイスです。 7番目のデバイス (RAS 非同期アダプター) は、ソフトウェアで列挙され\\たデバイス (SW\*) であり、必要になるまでインストールされません。

```
PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028&REV_78\4&BB7B4AE&0&60F0: 3Com 3C920 Integrated Fast
Ethernet Controller (3C905C-TX Compatible)
ROOT\MS_L2TPMINIPORT\0000                                   : WAN Miniport (L2TP)
ROOT\MS_NDISWANIP\0000                                      : WAN Miniport (IP)
ROOT\MS_PPPOEMINIPORT\0000                                  : WAN Miniport (PPPOE)
ROOT\MS_PPTPMINIPORT\0000                                   : WAN Miniport (PPTP)
ROOT\MS_PTIMINIPORT\0000                                    : Direct Parallel
SW\{EEAB7790-C514-11D1-B42B-00805FC1270E}\ASYNCMAC          : RAS Async Adapter
7 matching device(s) found.
```

次のコマンドは、以前の**Devcon findall**コマンドと同じパラメーターを使用して、 **devcon** find コマンドを実行して、 [**Devcon find**](devcon-find.md)と**devcon findall**操作を比較します。

```
devcon find =net
```

応答として、[DevCon] には、Net setup クラスに次の6つのデバイスが一覧表示されます。

```
PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028&REV_78\4&BB7B4AE&0&60F0: 3Com 3C920 Integrated Fast
Ethernet Controller (3C905C-TX Compatible)
ROOT\MS_L2TPMINIPORT\0000                                   : WAN Miniport (L2TP)
ROOT\MS_NDISWANIP\0000                                      : WAN Miniport (IP)
ROOT\MS_PPPOEMINIPORT\0000                                  : WAN Miniport (PPPOE)
ROOT\MS_PPTPMINIPORT\0000                                   : WAN Miniport (PPTP)
ROOT\MS_PTIMINIPORT\0000                                    : Direct Parallel
6 matching device(s) found.
```

現在インストールされているデバイスのみを返す**DevCon Find**コマンドは、デバイスがインストールされていないため、ソフトウェアで列挙されたデバイスの一覧を表示しません。

### <span id="ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools"></span><span id="DDK_EXAMPLE_23_DISPLAY_THE_FILTER_DRIVERS_FOR_A_SETUP_CLASS_TOOLS"></span><a name="ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools"></a>例 23:セットアップクラスのフィルタードライバーを表示する

次のコマンドは、 [**DevCon ClassFilter**](devcon-classfilter.md)操作を使用して、DiskDrive setup クラスの上位フィルタードライバーを表示します。 このコマンドには classfilter 演算子が含まれていないため、DevCon にはクラスのフィルタードライバーが表示されますが、変更されることはありません。

```
devcon classfilter DiskDrive upper
```

これに対して、DevCon は DiskDrive クラスの上位フィルタードライバーを表示し、変更されていないことを確認します。 この場合、DiskDrive セットアップクラスのデバイスでは、PartMgr の上位フィルタードライバーが使用されていることが表示されます。

```
Class filters unchanged.
    PartMgr
```

### <span id="ddk_example_24_add_a_filter_driver_to_a_setup_class_tools"></span><span id="DDK_EXAMPLE_24_ADD_A_FILTER_DRIVER_TO_A_SETUP_CLASS_TOOLS"></span><a name="ddk_example_24_add_a_filter_driver_to_a_setup_class_tools"></a>例 24:セットアップクラスへのフィルタードライバーの追加

次のコマンドは、 [**DevCon classfilter**](devcon-classfilter.md)操作を使用して、DiskDrive セットアップクラスの上位フィルタードライバーの一覧に架空のフィルター disklog を追加します。

このコマンドは、add after ( **+** ) classfilter 演算子を使用して、partmgr ドライバーの後に disklog ドライバーを読み込み、partmgr が既に処理したデータを受信できるようにします。

コマンドが開始されると、仮想カーソルは最初のフィルタードライバーの前に配置されます。 このファイルは特定のドライバーには配置されていないため、DevCon は、フィルタードライバーの一覧の末尾に Disklog ドライバーを追加します。

このコマンドでは、 **/r**パラメーターも使用します。このパラメーターは、クラスフィルターの変更を有効にする必要がある場合にシステムを再起動します。

```
devcon /r classfilter DiskDrive upper +Disklog
```

応答として、DiskDrive クラスの現在の上位フィルタードライバーが表示されます。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    Disklog
```

ドライバー名のスペルを間違えた場合、またはシステムにインストールされていないドライバーを追加しようとした場合、コマンドは失敗します。 DevCon は、ドライバーがサービスとして登録されている場合を除き、ドライバーが追加されません。ただし、ドライバーが Services\_レジストリサブ\\キーにサブキーを持っていない場合 (HKEY LOCAL\_MACHINE System\\CurrentControlSet\\サービス)。

次のコマンドは、この保護機能をテストします。 "Disklog" ではなく "Disklgg" を、DiskDrive クラスの上位フィルターの一覧に追加しようとします。 出力は、コマンドが失敗したことを示しています。

```
devcon /r classfilter DiskDrive upper +Disklgg
devcon failed.
```

### <span id="ddk_example_25_insert_a_filter_driver_in_the_class_list_tools"></span><span id="DDK_EXAMPLE_25_INSERT_A_FILTER_DRIVER_IN_THE_CLASS_LIST_TOOLS"></span><a name="ddk_example_25_insert_a_filter_driver_in_the_class_list_tools"></a>例 25:クラスの一覧にフィルタードライバーを挿入する

次のコマンドは、 [**DevCon classfilter**](devcon-classfilter.md)操作を使用して、DiskDrive セットアップクラスの上位フィルタードライバーの一覧に架空のフィルタードライバー myfilter を追加します。 コマンドは、の読み込み順序で、PartMgr と Disklog の間に MyFilter を配置します。

```
devcon /r classfilter DiskDrive upper @Disklog -MyFilter
```

次の一覧は、コマンドが送信される前の DiskDrive クラスのフィルタードライバーを示しています。

```
    PartMgr
    Disklog
```

最初のサブコマンド<strong>@Disklog</strong>は、配置演算子 ( **@** ) を使用して、disklog フィルタードライバーに仮想カーソルを配置します。 2番目のサブコマンドである **-myfilter**は、前に **-** 追加する演算子 () を使用して、disklog. sys の前に myfilter を追加します。

このコマンドでは、 **/r**パラメーターも使用します。このパラメーターは、クラスフィルターの変更を有効にする必要がある場合にシステムを再起動します。

この例では、配置演算子が不可欠です。 DevCon が classfilter サブコマンドを処理する前に、仮想カーソルはリストの先頭にあり、フィルタードライバーには配置されていません。 カーソルがドライバーに配置されて **+** いないときに before () 演算子を使用すると、そのドライバーが一覧の先頭に追加されます。 カーソルがドライバーに配置されて **-** いない場合に、after () 演算子を使用すると、ドライバーが一覧の末尾に追加されます。

応答として、DiskDrive クラスの現在の上位フィルタードライバーが表示されます。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    MyFilter
    Disklog
```

次のコマンドを使用して、MyFilter ドライバーを追加し、それを PartMgr と Disklog の間に配置することもできます。 この例では、最初のサブ<strong>@PartMgr</strong>コマンドは、仮想カーソルを partmgr フィルタードライバーに配置します。 2番目のサブコマンドである **+ Myfilter**は、後に追加演算子 (+) を使用して、partmgr の後に myfilter. sys を追加します。

```
devcon /r classfilter DiskDrive upper @PartMgr +MyFilter
```

### <span id="ddk_example_26_replace_a_filter_driver_tools"></span><span id="DDK_EXAMPLE_26_REPLACE_A_FILTER_DRIVER_TOOLS"></span><a name="ddk_example_26_replace_a_filter_driver_tools"></a>例 26:フィルタードライバーの置換

次のコマンドでは、 [**DevCon ClassFilter**](devcon-classfilter.md)操作を使用して、DiskDrive セットアップクラスのフィルタードライバーの一覧にある新しい改良されたバージョンの MyNewFilter を使用して、myfilter. sys の元のコピーを置き換えます。

```
devcon /r classfilter DiskDrive upper !MyFilter +MyNewFilter
```

次の一覧は、コマンドが送信される前の DiskDrive クラスのフィルタードライバーを示しています。

```
    PartMgr
    MyFilter
    Disklog
```

最初のサブコマンドは、delete 演算子 ( **!** ) を使用して、DiskDrive クラスの上位フィルタードライバーの一覧から myfilter を削除します。 (C:\\Windows\\System32\\Drivers ディレクトリの myfilter .sys ファイルには影響しません)。

2番目のサブコマンドは、後に **+** 追加演算子 () を使用して、削除されたドライバーが占有する位置に新しいフィルタードライバーを配置します。 Delete 演算子は、削除されたフィルターが適用されている位置にカーソルを置いて **-** いるため、before () **+** 演算子と after after () 演算子は同じ効果を持ちます。

このコマンドでは、 **/r**パラメーターも使用します。このパラメーターは、クラスフィルターの変更を有効にする必要がある場合にシステムを再起動します。

これに対して、DevCon は DiskDrive クラスの新しいクラスフィルター構成を表示します。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    MyNewFilter
    Disklog
```

### <span id="ddk_example_27_change_the_order_of_filter_drivers_tools"></span><span id="DDK_EXAMPLE_27_CHANGE_THE_ORDER_OF_FILTER_DRIVERS_TOOLS"></span><a name="ddk_example_27_change_the_order_of_filter_drivers_tools"></a>例 27:フィルタードライバーの順序を変更する

次のコマンドでは、 [**DevCon ClassFilter**](devcon-classfilter.md)操作を使用して、DiskDrive setup クラスのフィルタードライバーの順序を変更します。 具体的には、2番目と3番目のフィルタードライバーの順序を逆にします。

```
devcon /r classfilter DiskDrive upper !Disklog =@PartMgr +Disklog
```

次の一覧は、コマンドが送信される前の DiskDrive クラスのフィルタードライバーを示しています。 また、コマンドの意図された結果も示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[指定日付より前]</th>
<th align="left">After</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PartMgr</p></td>
<td align="left"><p>PartMgr</p></td>
</tr>
<tr class="even">
<td align="left"><p>MyNewFilter</p></td>
<td align="left"><p>Disklog</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Disklog</p></td>
<td align="left"><p>MyNewFilter</p></td>
</tr>
</tbody>
</table>

 

最初のサブコマンドは、delete 演算子 ( **!)** を使用して、一覧から disklog を削除します。 2番目のサブコマンドは、start 演算子 ( **=)** を使用して仮想カーソルを開始位置に戻し、配置演算子 ( **@)** を使用して partmgr ドライバーにカーソルを置きます。 仮想カーソルはリスト内を前方にのみ移動するため、start 演算子が必要です。 最後のサブコマンドは、後に追加演算子 ( **+)** を使用して、partmgr の後に disklog を追加します。

これに対して、DevCon は DiskDrive クラスの新しいクラスフィルター構成を表示します。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    Disklog
    MyNewFilter
```

### <span id="ddk_example_28_enable_a_particular_device_tools"></span><span id="DDK_EXAMPLE_28_ENABLE_A_PARTICULAR_DEVICE_TOOLS"></span><a name="ddk_example_28_enable_a_particular_device_tools"></a>例 28:特定のデバイスを有効にする

次のコマンドは、 [**DevCon Enable**](devcon-enable.md)操作を使用して、システムの問題を修正するために無効になっているプログラム可能な割り込みコントローラーを有効にします。 コントローラーのハードウェア id \*PNP0000 にはアスタリスクが含まれているため、コマンドは、単一引用符 ( **'** ) を使用して、コマンドで指定されているとおりにハードウェア id を正確に検索するように DevCon に指示します。 それ以外の場合、アスタリスクはワイルドカード文字として解釈されます。

```
devcon enable '*PNP0000
```

応答として、デバイスのデバイスインスタンス ID が表示され、デバイスを有効にするためにシステムを再起動する必要があることが示されます。

```
ACPI\PNP0000\4&B4063F4&0                                    : Enabled on reboot
Not all of 1 device(s) enabled, at least one requires reboot to complete the operation.
```

システムを再起動するには、手動で行うか、または[**DevCon Reboot**](devcon-reboot.md)操作を使用します。

次のコマンドは、 **/r**パラメーターを前のコマンドに追加します。 **/R**パラメーターを指定すると、操作を完了するために再起動が必要な場合にのみ、システムが再起動されます。

```
devcon /r enable '*PNP0000
```

これに対して、DevCon はデバイスを有効にし、システムを再起動して有効にします。

システムが起動したら、DevCon status コマンドを使用して、デバイスが有効になっていることを確認します。

```
devcon status '*PNP0000

ACPI\PNP0000\4&B4063F4&0
    Name: Programmable interrupt controller
    Driver is running.
```

### <span id="ddk_example_29_enable_devices_by_class_tools"></span><span id="DDK_EXAMPLE_29_ENABLE_DEVICES_BY_CLASS_TOOLS"></span><a name="ddk_example_29_enable_devices_by_class_tools"></a>例 29:クラス別にデバイスを有効にする

次のコマンドは、 [**DevCon Enable**](devcon-enable.md)コマンドで printer setup クラスを指定することにより、コンピューター上のすべてのプリンターデバイスを有効にします。 このコマンドには、有効にする必要がある場合にシステムを再起動する **/r**パラメーターが含まれています。

```
devcon /r enable =Printer
```

応答として、DevCon はプリンタクラスにあるプリンタのデバイスインスタンス ID を表示し、有効になっていることを報告します。 コマンドに **/r**パラメーターが含まれていても、プリンターを有効にするために再起動が必要ないため、システムは再起動されませんでした。

```
LPTENUM\HEWLETT-PACKARDDESKJET_1120C\1&7530F08&0&LPT1.4        : Enabled
1 device(s) enabled.
```

### <span id="ddk_example_30_disable_devices_by_an_id_pattern_tools"></span><span id="DDK_EXAMPLE_30_DISABLE_DEVICES_BY_AN_ID_PATTERN_TOOLS"></span><a name="ddk_example_30_disable_devices_by_an_id_pattern_tools"></a>例 30:ID パターンでデバイスを無効にする

次のコマンドは、 [**DevCon disable**](devcon-disable.md)操作を使用して、ローカルコンピューター上の USB デバイスを無効にします。 デバイスは、ハードウェア ID パターン (USB\*) によって識別されます。 このパターンは、ハードウェア ID または互換性のある ID が "USB" で始まる任意のデバイスと一致します。 コマンドには、 **/r**パラメーターが含まれています。このパラメーターは、無効化を有効にする必要がある場合にシステムを再起動します。

**メモ**  デバイスを無効にするために ID パターンを使用する前に、影響を受けるデバイスを決定します。 これを行うには、 **devcon status usb\\** * や * * devcon hwids USB\\* * * などの表示コマンドでパターンを使用します。

 

```
devcon /r disable USB*
```

応答として、[DevCon] には、USB デバイスのデバイスインスタンス Id と、無効になっているレポートが表示されます。 コマンドに **/r**パラメーターが含まれていても、デバイスを無効にするために再起動が必要ないため、システムは再起動されませんでした。

```
USB\ROOT_HUB\4&2A40B465&0
: Disabled
USB\ROOT_HUB\4&7EFA360&0
: Disabled
USB\VID_045E&PID_0039\5&29F428A4&0&2
: Disabled
3 device(s) disabled.
```

### <span id="ddk_example_31_disable_devices_by_device_instance_id_tools"></span><span id="DDK_EXAMPLE_31_DISABLE_DEVICES_BY_DEVICE_INSTANCE_ID_TOOLS"></span><a name="ddk_example_31_disable_devices_by_device_instance_id_tools"></a>例 31:デバイスインスタンス ID でデバイスを無効にする

次のコマンドは、 [**DevCon disable**](devcon-disable.md)操作を使用して、ローカルコンピューター上の USB デバイスを無効にします。 このコマンドは、各 ID の前にある at 文字 ( **@** ) で示されているデバイスインスタンス id でデバイスを識別します。 各デバイスインスタンス ID は、スペースで区別されます。

また、デバイスインスタンス id にはアンパサンド文字 ( **&** ) が含まれているため、引用符で囲まれています。 コマンドには、 **/r**パラメーターが含まれています。このパラメーターは、無効化を有効にする必要がある場合にシステムを再起動します。

```
devcon /r disable "@USB\ROOT_HUB\4&2A40B465&0" "@USB\ROOT_HUB\4&7EFA360&0" "@USB\VID_045E&PID_0039\5&29F428A4&0&2"
```

応答として、[DevCon] には、USB デバイスのデバイスインスタンス Id と、無効になっているレポートが表示されます。 コマンドに **/r**パラメーターが含まれていても、デバイスを無効にするために再起動が必要ないため、システムは再起動されませんでした。

```
USB\ROOT_HUB\4&2A40B465&0
: Disabled
USB\ROOT_HUB\4&7EFA360&0
: Disabled
USB\VID_045E&PID_0039\5&29F428A4&0&2
: Disabled
3 device(s) disabled.
```

### <span id="ddk_example_32_update_the_driver_for_communication_ports_tools"></span><span id="DDK_EXAMPLE_32_UPDATE_THE_DRIVER_FOR_COMMUNICATION_PORTS_TOOLS"></span><a name="ddk_example_32_update_the_driver_for_communication_ports_tools"></a>例 32:通信ポートのドライバーを更新する

次のコマンドは、 [**DevCon 更新**](devcon-update.md)操作を使用して、システム上の通信ポートの現在のデバイスドライバーを、テスト用の .inf ファイルで指定されたテストドライバーと置き換えます。 このコマンドは、ハードウェア ID 全体が PNP0501 ( \*アスタリスクを含む) であるデバイスにのみ影響します。

このコマンドを使用すると、システム上の署名されたドライバーをテストやトラブルシューティングのための代替ドライバーに置き換えたり、デバイスを同じドライバーの最新バージョンに関連付けたりすることができます。

```
devcon update c:\windows\inf\test.inf *PNP0501
```

応答として、ドライバーが Windows ロゴテストに合格していないことを示す**ハードウェアインストール**の警告が表示されます。 ダイアログボックスの **[続行]** ボタンをクリックすると、インストールが続行されます。

次に、[DevCon] で次の成功メッセージが表示されます。

```
Updating drivers for *PNP0501 from c:\windows\inf\test.inf.
Drivers updated successfully.
```

また、devcon [**UpdateNI**](devcon-updateni.md)操作 ( **devcon 更新**操作の非対話型バージョン) を使用してドライバーを更新することもできます。 **Devcon UpdateNI**操作は**devcon Update**操作と同じですが、応答を必要とし、プロンプトに対する既定の応答を想定しているすべてのユーザープロンプトが抑制される点が異なります。

次のコマンドは、 **DevCon UpdateNI**操作を使用して、テストドライバーをインストールします。

```
devcon updateni c:\windows\inf\test.inf *PNP0501
```

この場合、DevCon では**ハードウェアのインストール**の警告は表示されません。 代わりに、既定の応答である **[インストールの停止]** を前提としています。 その結果、DevCon はドライバーを更新できず、エラーメッセージが表示されます。

```
Updating drivers for *PNP0501 from c:\windows\inf\test.inf.
devcon failed.
```

### <span id="ddk_example_33_install_a_device_tools"></span><span id="DDK_EXAMPLE_33_INSTALL_A_DEVICE_TOOLS"></span><a name="ddk_example_33_install_a_device_tools"></a>例 33:デバイスをインストールする

次のコマンドは、 [**DevCon インストール**](devcon-install.md)操作を使用して、ローカルコンピューターにキーボードデバイスをインストールします。 このコマンドには、デバイス (PNP030b) の INF ファイルへの完全パスと、ハードウェア ID (\*) が含まれています。

```
devcon /r install c:\windows\inf\keyboard.inf *PNP030b
```

これに対して、DevCon は、デバイスがインストールされていることを報告します。つまり、新しいデバイス用のデバイスノードが作成され、デバイスのドライバーファイルが更新されています。

```
Device node created. Install is complete when drivers files are updated...
Updating drivers for *PNPO30b from c:\windows\inf\keyboard.inf
Drivers updated successfully.
```

### <span id="ddk_example_34_install_a_device_using_unattended_setup_tools"></span><span id="DDK_EXAMPLE_34_INSTALL_A_DEVICE_USING_UNATTENDED_SETUP_TOOLS"></span><a name="ddk_example_34_install_a_device_using_unattended_setup_tools"></a>例 34:無人セットアップを使用してデバイスをインストールする

次の例は、Microsoft Windows XP の無人インストール中に Microsoft Loopback Adapter をインストールする方法を示しています。

無人セットアップ中にこのデバイスをインストールするには、まず、次のファイルをフロッピーディスクに追加します。例: devcon と netloop\\.inf\\(\\C: Windows inf netloop .inf)。

次に、無人セットアップファイルの [ **\[GUIRunOnce\]** ] セクションに、次の DevCon コマンドを追加します。

```
a:\devcon /r install a:\Netloop.inf '*MSLOOP
```

このコマンドは\*、ハードウェア ID msloop を使用して、ループバックアダプタを識別します。 "\*Msloop" の前にある一重引用符文字は、文字列を文字どおりに解釈するように DevCon に指示します。つまり、ワイルドカード文字としてではなく、ハードウェア ID の一部としてアスタリスクを解釈します。

また、このコマンドは、インストール時に、DevCon が Netloop .inf ファイル (フロッピーディスク上) を使用することも指定します。 **/R**パラメーターを指定すると、インストールを完了するために再起動が必要な場合にのみ、コンピューターが再起動されます。

最後に、ネットワーク構成設定を無人セットアップファイルに追加し、無人セットアップを実行します。

### <span id="ddk_example_35_remove_devices_by_device_instance_id_pattern_tools"></span><span id="DDK_EXAMPLE_35_REMOVE_DEVICES_BY_DEVICE_INSTANCE_ID_PATTERN_TOOLS"></span><a name="ddk_example_35_remove_devices_by_device_instance_id_pattern_tools"></a>例 35:デバイスインスタンス ID パターン別にデバイスを削除する

次のコマンドは、 [**DevCon remove**](devcon-remove.md)操作を使用して、コンピューターからすべての USB デバイスを削除します。 デバイスは、"USB\\" 文字列で始まる任意のデバイスインスタンス id (レジストリパス) に一致するデバイスインスタンス id パターンによって識別されます。 At 文字 ( **@** ) は、デバイスインスタンス ID をハードウェア id または互換性 id と区別します。 このコマンドには、削除プロシージャを有効にする必要がある場合にシステムを再起動する **/r**パラメーターも含まれています。

**警告**  パターンを使用してデバイスを削除する前に、影響を受けているデバイスを特定します。 これを行う<strong>には、表示コマンドで、devcon status \\ <strong> @usb @usb \\ \</strong > * や devcon hwids \</strong > * などのパターンを使用します。

 

```
devcon /r remove @usb\*
```

応答として、[DevCon] は、削除したデバイスのデバイスインスタンス ID を表示します。

```
USB\ROOT_HUB\4&2A40B465&0                             : Removed
USB\ROOT_HUB\4&7EFA360&0                              : Removed
USB\VID_045E&PID_0039\5&29F428A4&0&2                  : Removed
3 device(s) removed.
```

### <span id="ddk_example_36_remove_a_particular_network_device_tools"></span><span id="DDK_EXAMPLE_36_REMOVE_A_PARTICULAR_NETWORK_DEVICE_TOOLS"></span><a name="ddk_example_36_remove_a_particular_network_device_tools"></a>例 36:特定のネットワークデバイスを削除する

次のコマンドは、 [**DevCon Remove**](devcon-remove.md)操作を使用して、ローカルコンピューターから NDISWAN ミニポートドライバーをアンインストールします。 このコマンドは、Net クラスを指定し、ハードウェア ID または互換性のある ID に "ndiswan" が含まれるクラスのデバイスを指定することによって検索を調整します。 このコマンドには、 **/r**パラメーターも含まれています。このパラメーターは、削除の手順を有効にするために再起動が必要な場合にシステムを再起動します。

**警告**  パターンを使用してデバイスを削除する前に、影響を受けるデバイスを決定します。 これを行うには、表示コマンドで、 **devcon status = \*net ndiswan\\** * または * * devcon hwids = net \*ndiswan\\* * * のパターンを使用します。

 

```
devcon /r remove =net *ndiswan*
```

応答として、[DevCon] には、削除したデバイスのデバイスインスタンス ID が表示されます。

```
ROOT\MS_NDISWANIP\0000 : Removed 1 device(s) removed.
```

### <span id="ddk_example_37_scan_the_computer_for_new_devices_tools"></span><span id="DDK_EXAMPLE_37_SCAN_THE_COMPUTER_FOR_NEW_DEVICES_TOOLS"></span><a name="ddk_example_37_scan_the_computer_for_new_devices_tools"></a>例 37:新しいデバイスのコンピューターをスキャンする

次のコマンドは、 [**DevCon 再スキャン**](devcon-rescan.md)操作を使用して、ローカルコンピューターで新しいデバイスをスキャンします。

```
devcon rescan
```

応答として、DevCon はシステムをスキャンしたが、新しいデバイスが検出されなかったことを報告します。

```
Scanning for new hardware.
Scanning completed.
```

また、リモートコンピューターでは、 **DevCon 再スキャン**コマンドを使用することもできます。 次のコマンドは、コマンドに **/m**パラメーターを追加することによって、リモートコンピューター Server01 の**DevCon 再スキャン**操作を実行します。

```
devcon /m:\\server01 rescan
```

### <span id="ddk_example_38_restart_a_device_tools"></span><span id="DDK_EXAMPLE_38_RESTART_A_DEVICE_TOOLS"></span><a name="ddk_example_38_restart_a_device_tools"></a>例 38:デバイスを再起動する

次のコマンドは、 [**DevCon restart**](devcon-restart.md)操作を使用して、ローカルコンピューター上のループバックアダプターを再起動します。 このコマンドは、検索を Net setup クラスに限定し、そのクラス内で、ループバックアダプタのデバイスインスタンス ID (**ルート\\\*msloop\\0000**) を指定します。 At 文字 ( **@** ) は、デバイスインスタンス ID として文字列を識別します。 単一引用符文字 ( **'** ) は、リテラル検索を要求します。これにより、DEVCON は ID のアスタリスクをワイルドカード文字として解釈できなくなります。

```
devcon restart =net @'ROOT\*MSLOOP\0000
```

応答として、デバイスのデバイスインスタンス ID を表示し、結果を報告します。

```
ROOT\*MSLOOP\0000                                              : Restarted
1 device(s) restarted.
```

### <span id="ddk_example_39_reboot_the_local_computer_tools"></span><span id="DDK_EXAMPLE_39_REBOOT_THE_LOCAL_COMPUTER_TOOLS"></span><a name="ddk_example_39_reboot_the_local_computer_tools"></a>例 39:ローカルコンピューターを再起動する

次のコマンドは、 [**DevCon reboot**](devcon-reboot.md)操作を使用して、ローカルコンピューター上のオペレーティングシステムを再起動し、再起動をハードウェアインストールに関連付けます。 **/R**パラメーターとは異なり、 **DevCon の再起動**操作は、別の操作からのリターンコードに依存しません。

このコマンドは、システムを再起動する必要があるスクリプトおよびバッチファイルに含めることができます。

```
devcon reboot
```

応答として、DevCon はコンピューターを再起動している (ローカルコンピューターを再起動している) ことを示すメッセージを表示します。


DevCon は、標準の**ExitWindowsEx**関数を使用して再起動します。 ユーザーがコンピューター上のファイルを開いている場合、またはプログラムが終了しない場合、ユーザーがファイルを閉じるかプロセスを終了するためにシステムプロンプトに応答するまで、システムは再起動されません。

### <span id="ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools"></span><span id="DDK_EXAMPLE_40_ASSIGN_A_HARDWARE_ID_TO_A_LEGACY_DEVICE_TOOLS"></span><a name="ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools"></a>例 40:レガシデバイスにハードウェア ID を割り当てる

次のコマンドでは、 [**DevCon SetHwID**](devcon-sethwid.md)操作を使用して、ハードウェア ID、ビープ音をレガシビープ音デバイスに割り当てています。

このコマンドは、デバイスのデバイスインスタンス ID を\\\_\\使用します。これは、ビープ音のレガシデバイスにハードウェア id も互換性 id もないためです。 この例では、at **@** 文字 () を使用して、文字列がデバイスインスタンス ID であることを示しています。

このコマンドでは、シンボルパラメーターを使用して ID を配置することはありません。 既定では、[DevCon] はハードウェア ID リストの末尾に新しいハードウェア Id を追加します。 この場合、デバイスには他のハードウェア Id がないため、配置は関係ありません。

```
devcon sethwid @ROOT\LEGACY_BEEP\0000 := beep
```

応答として、デバイスのハードウェア ID の一覧にビープ音が追加されたことを示すメッセージが表示されます。 また、結果として得られるハードウェア ID の一覧も表示されます。 この場合、一覧にはハードウェア ID が1つだけあります。

```
ROOT\LEGACY_BEEP\0000                              : beep
Modified 1 hardware ID(s).
```

### <span id="ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com"></span><span id="DDK_EXAMPLE_41_ADD_A_HARDWARE_ID_TO_ALL_LEGACY_DEVICES_ON_A_REMOTE_COM"></span><a name="ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com"></a>例 41:リモートコンピューター上のすべてのレガシデバイスにハードウェア ID を追加する

次のコマンドは、 [**DevCon SetHwID**](devcon-sethwid.md)操作を使用して、Server1 リモートコンピューター上のすべてのレガシデバイスのハードウェア id の一覧に、ハードウェア id (レガシ) を追加します。

このコマンドは、 **-** symbol パラメーターを使用して、デバイスのハードウェア id リストの末尾に新しいハードウェア id を追加します。デバイスの1つに優先ハードウェア id が作成されている場合に使用します。 **/M**パラメーターを使用して、リモートコンピューターを指定します。 また、デバイス<strong>インスタンス id パターン ( @ROOT \\レガシ\</strong >) を使用して、<em>コンピューター上のレガシデバイス、つまり、デバイスインスタンス id が **ROOT\\で始まるすべてのデバイスを識別します。レガシ</em>* 。

```
devcon /m:\\Server1 sethwid @ROOT\LEGACY* := -legacy
```

応答として、該当するすべてのデバイスについて、結果として得られるハードウェア ID の一覧が表示されます。

```
ROOT\LEGACY_AFD\0000                                        : legacy
ROOT\LEGACY_BEEP\0000                                    : beep,legacy
ROOT\LEGACY_CRCDISK\0000                                    : legacy
ROOT\LEGACY_DMBOOT\0000                                     : legacy
ROOT\LEGACY_DMLOAD\0000                                     : legacy
ROOT\LEGACY_FIPS\0000                                       : legacy
...
ROOT\LEGACY_WANARP\0000                                     : legacy
Modified 27 hardware ID(s).
```

同じハードウェア ID をデバイスのグループに割り当てた後、他の DevCon 操作を使用して、1つのコマンドでデバイスを表示および変更できます。

たとえば、次のコマンドは、すべてのレガシデバイスの状態を表示します。

```
devcon status legacy
```

### <span id="ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot"></span><span id="DDK_EXAMPLE_42_DELETE_A_HARDWARE_ID_FROM_ALL_LEGACY_DEVICES_ON_A_REMOT"></span><a name="ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot"></a>例 42:リモートコンピューター上のすべてのレガシデバイスからハードウェア ID を削除する

次のコマンドは、 [**DevCon SetHwID**](devcon-sethwid.md)操作を使用して、Server1 リモートコンピューター上のすべてのレガシデバイスのハードウェア id の一覧から、ハードウェア id (**レガシ**) を削除します。

このコマンドは、 **/m**パラメーターを使用してリモートコンピューターを指定します。 ハードウェア ID (**レガシ**) を使用して、そのハードウェア id を持つすべてのデバイスを識別します。 次に、を使用します **。** **レガシ**ハードウェア ID を削除するシンボルパラメーター。

```
devcon /m:\\Server1 sethwid legacy := !legacy
```

応答として、該当するすべてのデバイスについて、結果として得られるハードウェア ID の一覧が表示されます。

```
ROOT\LEGACY_AFD\0000                                        :
ROOT\LEGACY_BEEP\0000                                    : beep
ROOT\LEGACY_CRCDISK\0000                                    :
ROOT\LEGACY_DMBOOT\0000                                     :
ROOT\LEGACY_DMLOAD\0000                                     :
ROOT\LEGACY_FIPS\0000                                       :
...
ROOT\LEGACY_WANARP\0000                                     :
Modified 27 hardware ID(s).
```

### <span id="ddk_example_43_add_delete_and_replace_hardwareids_tools"></span><span id="DDK_EXAMPLE_43_ADD_DELETE_AND_REPLACE_HARDWAREIDS_TOOLS"></span><a name="ddk_example_43_add_delete_and_replace_hardwareids_tools"></a>例 43:ハードウェア Id の追加、削除、交換

次の一連の例は、 [**DevCon SetHwID**](devcon-sethwid.md)操作のさまざまな機能を使用する方法を示しています。

このシリーズでは、デバイスインスタンス ID、**ルート\\devicex\\0000**を使用して、架空のデバイスである devicex を使用します。 DevCon を使用する前に、デバイスには次のハードウェア Id の一覧があります。

```
Hw3 Hw4
```

次のコマンドは、 **+** シンボルを使用して、 **Hw1**と**Hw2**を devicex のハードウェア id のリストの先頭に追加します。 **Hw2**は既に一覧に表示されているため、移動され、追加されることはありません。 このコマンドは、id の前のアット文字 ( **@** ) で示されているように、デバイスのインスタンス ID でデバイスを識別します。

```
devcon sethwid @ROOT\DEVICEX\0000 := +Hw1 Hw2
```

応答として、デバイスの新しいハードウェア ID の一覧が表示されます。 **Hw1**と**Hw2**は、指定された順序でリストの先頭に表示されることに注意してください。

```
ROOT\DEVICEX\0000                         : Hw1,Hw2,Hw3,Hw4
Modified 1 hardware ID(s).
```

また、DevCon は、1つのハードウェア ID リスト、つまり1つのデバイスのハードウェア ID リストを変更したことを報告します。

次のコマンドは、を使用します **。** **Hw1**ハードウェア ID を削除するためのシンボル。 次に、シンボルパラメーターを指定せずに、ハードウェア ID **Hw5**を一覧表示します。 シンボルパラメーターを指定しない場合、SetHwID は、デバイスのハードウェア ID リストの末尾にハードウェア ID を追加します。

このコマンドは、 **DevCon SetHwID**操作の他のシンボルパラメーターとは異なり、 **!** シンボルは、そのプレフィックスとなるハードウェア ID にのみ適用されます。

```
devcon sethwid @ROOT\DeviceX\0000 := !Hw1 Hw5
```

応答として、[DevCon] のハードウェア ID の一覧が表示されます。

```
ROOT\DEVICEX\0000                         : Hw2,Hw3,Hw4,Hw5
Modified 1 hardware ID(s).
```

次のコマンドは、= パラメーターを使用して、リスト内のすべてのハードウェア id を、DeviceX の1つのハードウェア ID **Devx**に置き換えます。

```
devcon sethwid @ROOT\DeviceX\0000 := =DevX
```

応答として、[DevCon] のハードウェア ID の一覧が表示されます。

```
ROOT\DEVICEX\0000                         : DevX
Modified 1 hardware ID(s).
```

成功メッセージは、1つのデバイスのハードウェア ID が DevCon によって変更されたことを示します。

### <span id="ddk_example_44_forcibly_update_the_hal_tools"></span><span id="DDK_EXAMPLE_44_FORCIBLY_UPDATE_THE_HAL_TOOLS"></span><a name="ddk_example_44_forcibly_update_the_hal_tools"></a>例 44:HAL を強制的に更新する

次の例は、DevCon を使用してコンピューター上の HAL を更新する方法を示しています。 この例で、テスト担当者は、コンピューターに最適なユニプロセッサ APCI APIC HAL を、テスト目的でマルチプロセッサ APCI APIC HAL に置き換えます。

最初のコマンドは、 [**DevCon SetHwID**](devcon-sethwid.md)操作を使用して、HAL のハードウェア id**を\_acpiapic up**(ユニプロセッサ hal のハードウェア id)**から\_acpiapic mp**(マルチプロセッサ hal のハードウェア id) に変更します。

HAL の INF ファイルには、ユニプロセッサとマルチプロセッサの両方の Hal のドライバーが含まれているため、ハードウェア ID を変更する必要があります。 システムは、デバイスのハードウェア ID に基づいて、INF ファイルから最適なドライバーを選択します。 ハードウェア ID を変更しない場合、 **DevCon Update**コマンドは単にユニプロセッサ HAL ドライバーを再インストールします。

次のコマンドでは、id の前 **@** の文字で示されているように、コマンドは、そのインスタンス id、 **ROOT\\ACPI\_\\HAL 0000**で HAL を識別します。 このコマンドは、 **+** 文字を使用して、 **acpiapic\_mp**を HAL の一覧の最初のハードウェア ID にします。 次に、を使用します **。** HAL の id の一覧から**acpiapic\_up**ハードウェア ID を削除する文字。

```
devcon sethwid @ROOT\ACPI_HAL\0000 := +acpiapic_mp !acpiapic_up
```

応答として、[DevCon] には、HAL の次の新しいハードウェア ID の一覧が表示されます。

```
ROOT\ACPI_HAL\0000                         : acpiapic_mp
Modified 1 hardware ID(s).
```

次のコマンドは、 [**DevCon 更新**](devcon-update.md)操作を使用して、HAL のドライバーを更新します。

```
devcon update c:\windows\inf\hal.inf acpiapic_mp
```

次に、[DevCon] で次の成功メッセージが表示されます。

```
Updating drivers for acpiapic_mp from c:\windows\inf\hal.inf.
Drivers updated successfully.
```

 

 






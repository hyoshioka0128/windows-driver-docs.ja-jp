---
title: デバイス コンソール (DevCon.exe) の例
description: デバイス コンソール (DevCon.exe) の例
ms.assetid: 5af1e777-04ba-4e83-b239-f568a02a9460
keywords:
- DevCon WDK、例
- デバイス コンソール WDK、例
- WDK DevCon の例
- WDK DevCon コマンド
- デバイス コンソール WDK、コマンド
- WDK DevCon コマンド
- 例 44 HAL を強制的に更新します。
- HAL の更新の例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23508e68c050334b1090993d5b3b00921d9b4ed7
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350273"
---
# <a name="device-console-devconexe-examples"></a>デバイス コンソール (DevCon.exe) の例


## <span id="ddk_devcon_examples_tools"></span><span id="DDK_DEVCON_EXAMPLES_TOOLS"></span>


ここでは、次のデバイスのコンソール (DevCon.exe) コマンドの例を示します。

### <a name="span-iddevconhwidsspanspan-iddevconhwidsspandevcon-hwids"></a><span id="devcon_hwids"></span><span id="DEVCON_HWIDS"></span>DevCon HwIDs

[例 1:すべてのハードウェア Id を検索します。](#ddk_example_1_find_all_hardware_ids_tools)

[例 2:パターンを使用して、ハードウェア Id を検索します。](#ddk_example_2_find_hardware_ids_by_using_a_pattern_tools)

[例 3:クラスを使用して、ハードウェア Id を検索します。](#ddk_example_3_find_hardware_ids_by_using_a_class_tools)

### <a name="span-iddevconclassesspanspan-iddevconclassesspandevcon-classes"></a><span id="devcon_classes"></span><span id="DEVCON_CLASSES"></span>DevCon クラス

[例 4:ローカル コンピューターのリスト クラス](#ddk_example_4_list_classes_on_the_local_computer_tools)

[例 5:リモート コンピューター上のリスト クラス](#ddk_example_5_list_classes_on_the_remote_computer_tools)

### <a name="span-iddevconlistclassspanspan-iddevconlistclassspandevcon-listclass"></a><span id="devcon_listclass"></span><span id="DEVCON_LISTCLASS"></span>DevCon ListClass

[例 6:デバイス セットアップ クラスでデバイスを一覧表示します。](#ddk_example_6_list_the_devices_in_a_device_setup_class_tools)

[例 7:リモート コンピューター上の複数のクラス内のデバイスを一覧表示します。](#ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute)

### <a name="span-iddevcondriverfilesspanspan-iddevcondriverfilesspandevcon-driverfiles"></a><span id="devcon_driverfiles"></span><span id="DEVCON_DRIVERFILES"></span>DevCon DriverFiles

[例 8:すべてのドライバー ファイルを一覧表示します。](#ddk_example_8_list_all_driver_files_tools)

[例 9:特定のデバイスのドライバー ファイルを一覧表示します。](#ddk_example_9_list_the_driver_files_of_a_particular_device_tools)

### <a name="span-iddevcondrivernodesspanspan-iddevcondrivernodesspandevcon-drivernodes"></a><span id="devcon_drivernodes"></span><span id="DEVCON_DRIVERNODES"></span>DevCon DriverNodes

[例 10:ハードウェア ID のパターンでドライバー パッケージの一覧](#ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools)

[例 11:デバイス インスタンス ID のパターンでドライバー パッケージの一覧](#ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool)

### <a name="span-iddevconresourcesspanspan-iddevconresourcesspandevcon-resources"></a><span id="devcon_resources"></span><span id="DEVCON_RESOURCES"></span>DevCon リソース

[12 の例:デバイスのクラスのリソースを一覧表示](#ddk_example_12_list_resources_of_a_class_of_devices_tools)

[13 の使用例:デバイス ID でリモート コンピューター上のリソースを一覧表示](#ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too)

### <a name="span-iddevconstackspanspan-iddevconstackspandevcon-stack"></a><span id="devcon_stack"></span><span id="DEVCON_STACK"></span>DevCon スタック

[14 の使用例:記憶装置のドライバー スタックを表示します。](#ddk_example_14_display_the_driver_stack_for_storage_devices_tools)

[15 の使用例:デバイスのセットアップ クラスを見つける](#ddk_example_15_find_the_setup_class_of_a_device_tools)

[16 の使用例:リモート コンピューターに関連するデバイスの履歴を表示します。](#ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu)

### <a name="span-iddevconstatusspanspan-iddevconstatusspandevcon-status"></a><span id="devcon_status"></span><span id="DEVCON_STATUS"></span>DevCon 状態

[17 の使用例:ローカル コンピューターのすべてのデバイスの状態を表示します。](#ddk_example_17_display_the_status_of_all_devices_on_the_local_computer)

[18 の使用例:デバイス インスタンス ID の状態を表示します。](#ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to)

[19 の使用例:リモート コンピューターに関連するデバイスの状態を表示します。](#ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu)

### <a name="span-iddevconfindspanspan-iddevconfindspandevcon-find"></a><span id="devcon_find"></span><span id="DEVCON_FIND"></span>DevCon 検索

[20 の使用例:ハードウェア ID のパターンでデバイスを検索します。](#ddk_example_20_find_devices_by_hardware_id_pattern_tools)

[21 の使用例:デバイス インスタンス ID またはクラスによってデバイスを検索します。](#ddk_example_21_find_devices_by_device_instance_id_or_class_tools)

### <a name="span-iddevconfindallspanspan-iddevconfindallspandevcon-findall"></a><span id="devcon_findall"></span><span id="DEVCON_FINDALL"></span>DevCon FindAll

[22 の使用例:検索 (および すべて検索) デバイス セットアップ クラス](#ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools)

### <a name="span-iddevconclassfilterspanspan-iddevconclassfilterspandevcon-classfilter"></a><span id="devcon_classfilter"></span><span id="DEVCON_CLASSFILTER"></span>DevCon ClassFilter

[23 の使用例:セットアップ クラスに対するドライバーだけを表示します。](#ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools)

[24 の使用例:フィルター ドライバー セットアップ クラスを追加します。](#ddk_example_24_add_a_filter_driver_to_a_setup_class_tools)

[25 の使用例:[クラス] 一覧で、フィルター ドライバーを挿入します。](#ddk_example_25_insert_a_filter_driver_in_the_class_list_tools)

[26 の使用例:フィルター ドライバーを置き換える](#ddk_example_26_replace_a_filter_driver_tools)

[27 の使用例:フィルター ドライバーの順序を変更します。](#ddk_example_27_change_the_order_of_filter_drivers_tools)

### <a name="span-iddevconenablespanspan-iddevconenablespandevcon-enable"></a><span id="devcon_enable"></span><span id="DEVCON_ENABLE"></span>DevCon 有効にします。

[28 の使用例:特定のデバイスを有効にします。](#ddk_example_28_enable_a_particular_device_tools)

[29 の使用例:クラスによってデバイスを有効にします。](#ddk_example_29_enable_devices_by_class_tools)

### <a name="span-iddevcondisablespanspan-iddevcondisablespandevcon-disable"></a><span id="devcon_disable"></span><span id="DEVCON_DISABLE"></span>DevCon 無効にします。

[30 の使用例:ID、パターンによってデバイスを無効にします。](#ddk_example_30_disable_devices_by_an_id_pattern_tools)

[31 の使用例:デバイス インスタンス ID でデバイスを無効にします。](#ddk_example_31_disable_devices_by_device_instance_id_tools)

### <a name="span-iddevconupdateandupdatenispanspan-iddevconupdateandupdatenispandevcon-update-and-updateni"></a><span id="devcon_update_and_updateni"></span><span id="DEVCON_UPDATE_AND_UPDATENI"></span>DevCon Update および UpdateNI

[例: 32:通信ポートのドライバーを更新します。](#ddk_example_32_update_the_driver_for_communication_ports_tools)

[例 44:HAL を強制的に更新します。](#ddk_example_44_forcibly_update_the_hal_tools)

### <a name="span-iddevconinstallspanspan-iddevconinstallspandevcon-install"></a><span id="devcon_install"></span><span id="DEVCON_INSTALL"></span>DevCon インストール

[33 の使用例:デバイスをインストールします。](#ddk_example_33_install_a_device_tools)

[34 の使用例:無人セットアップを使用してデバイスをインストールします。](#ddk_example_34_install_a_device_using_unattended_setup_tools)

### <a name="span-iddevconremovespanspan-iddevconremovespandevcon-remove"></a><span id="devcon_remove"></span><span id="DEVCON_REMOVE"></span>DevCon の削除

[35 の使用例:デバイス インスタンス ID のパターンによってデバイスを削除します。](#ddk_example_35_remove_devices_by_device_instance_id_pattern_tools)

[36 の使用例:特定のネットワーク デバイスを削除します。](#ddk_example_36_remove_a_particular_network_device_tools)

### <a name="span-iddevconrescanspanspan-iddevconrescanspandevcon-rescan"></a><span id="devcon_rescan"></span><span id="DEVCON_RESCAN"></span>DevCon 再スキャン

[37 の使用例:新しいデバイスには、コンピューターをスキャンします。](#ddk_example_37_scan_the_computer_for_new_devices_tools)

### <a name="span-iddevconrestartspanspan-iddevconrestartspandevcon-restart"></a><span id="devcon_restart"></span><span id="DEVCON_RESTART"></span>DevCon 再起動

[38 の使用例:デバイスを再起動します。](#ddk_example_38_restart_a_device_tools)

### <a name="span-iddevconstatus2spanspan-iddevconstatus2spandevcon-status"></a><span id="devcon_status2"></span><span id="DEVCON_STATUS2"></span>DevCon 状態

[39 の使用例:ローカル コンピューターを再起動します。](#ddk_example_39_reboot_the_local_computer_tools)

### <a name="span-iddevconsethwidspanspan-iddevconsethwidspandevcon-sethwid"></a><span id="devcon_sethwid"></span><span id="DEVCON_SETHWID"></span>DevCon SetHwID

[40 の使用例:レガシ デバイスのハードウェア ID を割り当てる](#ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools)

[41 の使用例:リモート コンピューター上のすべてのレガシ デバイスにハードウェア ID を追加します。](#ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com)

[42 の使用例:リモート コンピューター上のすべてのレガシ デバイスからのハードウェア ID を削除します。](#ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot)

[43 の使用例:追加、削除、およびハードウェア Id を置き換えます](#ddk_example_43_add_delete_and_replace_hardwareids_tools)

[例 44:HAL を強制的に更新します。](#ddk_example_44_forcibly_update_the_hal_tools)

### <a name="span-iddevcondpadddpdeleteddpenumspanspan-iddevcondpadddpdeleteddpenumspandevcon-dpadd-dpdeleted-dpenum"></a><span id="devcon_dp_add__dp_deleted__dp_enum"></span><span id="DEVCON_DP_ADD__DP_DELETED__DP_ENUM"></span>DevCon dp\_dp を追加します\_削除されると、dp\_列挙型。

[45 の使用例:追加して、ドライバー パッケージを削除します。](example-45--add-and-remove-driver-packages.md)

### <span id="ddk_example_1_find_all_hardware_ids_tools"></span><span id="DDK_EXAMPLE_1_FIND_ALL_HARDWARE_IDS_TOOLS"></span><a name="ddk_example_1_find_all_hardware_ids_tools"></a>例 1:すべてのハードウェア Id を検索します。

DevCon 操作 Id を使用して、最初に、共通のデバイスを識別する ID のパターンのステップあるため DevCon を使用して、コンピューターのデバイスのハードウェア ID の参照ファイルを作成します。

次のコマンドを使用して、 [ **DevCon HwIDs** ](devcon-hwids.md)操作で、Id とデバイスの説明を返します。 使われているワイルドカード文字 (* *\\* * *) をローカル コンピューター上のすべてのデバイスを表します。

```
devcon hwids *
```

出力は、時間のかかると使用を繰り返しはであるために、参照用のテキスト ファイルに出力を保存します。

次のコマンドは、ワイルドカード文字 (**\\* * *) をコンピューター上のすべてのデバイスを表します。リダイレクト文字を使用して (*<em>&gt;</em>*) を hwids.txt ファイルで、コマンドの出力を保存します。

```
devcon hwids * > hwids.txt
```

次のコマンドは、Server01 リモート コンピューターのハードウェア デバイスの Id を検索します。 使用して、 **/m**パラメーターをリモート コンピューターの名前を指定します。 コマンドは、server01 に出力をリダイレクト\_hwids.txt ファイルを後で参照します。

**注**  このコマンドは、ユーザーがリモート コンピューターで必要なアクセス許可が失敗します。 DevCon コマンドをリモート コンピューターで実行するには、グループ ポリシー設定は、リモート コンピューター上で実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista および Windows 7 を実行するコンピューター、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。 Windows Driver Kit (WDK) 8.1 と Windows Driver Kit (WDK) 8 を実行するコンピューター、リモート アクセスでは使用できません。

 

```
devcon /m:\\server01 hwids * > server01_hwids.txt
```

### <span id="ddk_example_2_find_hardware_ids_by_using_a_pattern_tools"></span><span id="DDK_EXAMPLE_2_FIND_HARDWARE_IDS_BY_USING_A_PATTERN_TOOLS"></span><a name="ddk_example_2_find_hardware_ids_by_using_a_pattern_tools"></a>例 2:パターンを使用して、ハードウェア Id を検索します。

特定のデバイスのハードウェア Id を検索するには、ハードウェア ID またはパターン、互換性のある ID やパターン、デバイスのインスタンス ID またはパターン、またはデバイス セットアップ クラスの名前を入力します。

次のコマンドを使用して、 **DevCon HwIDs**操作およびフロッピー ディスクのハードウェア Id を検索するパターンは、コンピューターのドライブです。 (対象ユーザーにデバイスのデバイス id のいずれかで、パターンが表示されることです。)コマンドは、使われているワイルドカード文字 (* *\\* * *) をその可能性があります前または次の Id のいずれかで「フロッピー」という単語のすべての文字を表します。

```
devcon hwids *floppy*
```

応答、DevCon は、コンピューターのデバイス インスタンス ID、ハードウェア ID、およびフロッピー ディスク ドライブの互換性のある ID を表示します。 後続の DevCon コマンドでは、これらの Id を使用できます。

```
FDC\GENERIC_FLOPPY_DRIVE\5&39194F6D&0&0
    Name: Floppy disk drive
    Hardware ID's:
        FDC\GENERIC_FLOPPY_DRIVE
    Compatible ID's:
        GenFloppyDisk
1 matching device(s) found.
```

この場合は、ハードウェア ID または互換性 ID、コンピューター上の 1 つだけのデバイスの"floppy"という語句が発生します。 1 つ以上のデバイスの ID で発生した場合、出力に"floppy"にその Id を持つすべてのデバイスが表示されます。

### <span id="ddk_example_3_find_hardware_ids_by_using_a_class_tools"></span><span id="DDK_EXAMPLE_3_FIND_HARDWARE_IDS_BY_USING_A_CLASS_TOOLS"></span><a name="ddk_example_3_find_hardware_ids_by_using_a_class_tools"></a>例 3:クラスを使用して、ハードウェア Id を検索します。

次のコマンドを使用して、 [ **DevCon HwIDs** ](devcon-hwids.md)操作と、デバイスは、ポートのデバイス セットアップ クラスのすべてのデバイスのハードウェア Id を検索するクラスをセットアップします。 等号 (=) (**=**)、クラス名の前に、ID ではない、クラスであることを示します

```
devcon hwids =ports
```

応答では、DevCon には、ハードウェア Id およびポートのセットアップ クラスの 3 つのデバイスの互換性 Id が表示されます。

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

### <span id="ddk_example_4_list_classes_on_the_local_computer_tools"></span><span id="DDK_EXAMPLE_4_LIST_CLASSES_ON_THE_LOCAL_COMPUTER_TOOLS"></span><a name="ddk_example_4_list_classes_on_the_local_computer_tools"></a>例 4:ローカル コンピューターのリスト クラス

DevCon 操作では、デバイス セットアップ クラスを使用して、デバイスを識別、ため、コンピューターにデバイスのデバイス セットアップ クラスの参照ファイルを作成すると便利です。

次のコマンドを使用して、 [ **DevCon クラス**](devcon-classes.md)操作で、コンピューターの一覧とすべてのクラスの説明を返します。

```
devcon classes
```

出力は、時間のかかると使用を繰り返しはであるために、参照用のテキスト ファイルに出力を保存します。

次のコマンドは、コンピューター上のすべてのデバイス クラスを表示します。 リダイレクト文字を使用して (**&gt;**) classes.txt ファイルで、コマンドの出力を保存します。

```
devcon classes > classes.txt
```

### <span id="ddk_example_5_list_classes_on_the_remote_computer_tools"></span><span id="DDK_EXAMPLE_5_LIST_CLASSES_ON_THE_REMOTE_COMPUTER_TOOLS"></span><a name="ddk_example_5_list_classes_on_the_remote_computer_tools"></a>例 5:リモート コンピューター上のリスト クラス

次のコマンドを使用して、 [ **DevCon クラス**](devcon-classes.md)を Server01 リモート コンピューター上のデバイス セットアップ クラスを一覧表示操作。

```
devcon /m:\\server01 classes
```

出力は、時間のかかると使用を繰り返しはであるために、参照用のテキスト ファイルに出力を保存します。

次のコマンドはリダイレクト文字を使用して (**&gt;**)、server01 にコマンドの出力を保存する\_classes.txt ファイル。

```
devcon /m:\\server01 classes > server01_classes.txt
```

### <span id="ddk_example_6_list_the_devices_in_a_device_setup_class_tools"></span><span id="DDK_EXAMPLE_6_LIST_THE_DEVICES_IN_A_DEVICE_SETUP_CLASS_TOOLS"></span><a name="ddk_example_6_list_the_devices_in_a_device_setup_class_tools"></a>例 6:デバイス セットアップ クラスでデバイスを一覧表示します。

次のコマンドを使用して、 [ **DevCon ListClass** ](devcon-listclass.md) Net、ネットワーク アダプターに対するデバイス セットアップ クラス内のデバイスを一覧表示する操作。

```
devcon listclass net
```

応答では、DevCon はデバイス インスタンス ID と Net セットアップ クラス内の各デバイスの説明を表示します。

```
Listing 6 device(s) for setup class "Net" (Network adapters).
PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028&REV_78\4&BB7B4AE&0&60F0: 3Com 3C920 Integrated Fast Ethernet Controller (3C905C-TX Compatible)
ROOT\MS_L2TPMINIPORT\0000                                   : WAN Miniport (L2TP)
ROOT\MS_NDISWANIP\0000                                      : WAN Miniport (IP)
ROOT\MS_PPPOEMINIPORT\0000                                  : WAN Miniport (PPPOE)
ROOT\MS_PPTPMINIPORT\0000                                   : WAN Miniport (PPTP)
ROOT\MS_PTIMINIPORT\0000                                    : Direct Parallel
```

この表示では、興味のあるは提供しません Net セットアップ クラスのデバイスのハードウェア Id。 次のコマンドを使用して、 [ **DevCon HwIDs** ](devcon-hwids.md) Net セットアップ クラスのデバイスを一覧表示する操作。 **DevCon HwIDs**コマンド、クラス名の前に等号 (**=**) クラスの場合、ID ではないことを示すために

```
devcon hwids =net
```

結果の表示では、Net クラス内のデバイスの一覧し、クラスにはデバイス インスタンス ID には、ハードウェア Id、デバイスの互換性のある Id が含まれます。

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

### <span id="ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute"></span><span id="DDK_EXAMPLE_7_LIST_THE_DEVICES_IN_MULTIPLE_CLASSES_ON_A_REMOTE_COMPUTE"></span><a name="ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute"></a>例 7:リモート コンピューター上の複数のクラス内のデバイスを一覧表示します。

次のコマンドを使用して、 [ **DevCon ListClass** ](devcon-listclass.md)をディスク ドライブ、cd-rom ドライブ、およびテープ デバイスを一覧表示操作では、リモート コンピューターを Server01 上にクラスします。

```
devcon /m:\\server01 listclass diskdrive cdrom tapedrive
```

応答、DevCon は、リモート コンピューターでこれらのクラス内のデバイスを表示します。

```
Listing 1 device(s) for setup class "DiskDrive" (Disk drives) on \\server01.
IDE\DISKWDC_WD204BA_____________________________16.13M16\4457572D414D3730323136333938203120202020: WDC WD204BA
Listing 1 device(s) for setup class "CDROM" (DVD/CD-ROM drives) on \\server01.
IDE\CDROMSAMSUNG_DVD-ROM_SD-608__________________2.2_____\4&13B4AFD&0&0.0.0: SAMSUNG DVD-ROM SD-608
No devices for setup class "TapeDrive" (Tape drives) on \\server01.
```

### <span id="ddk_example_8_list_all_driver_files_tools"></span><span id="DDK_EXAMPLE_8_LIST_ALL_DRIVER_FILES_TOOLS"></span><a name="ddk_example_8_list_all_driver_files_tools"></a>例 8:すべてのドライバー ファイルを一覧表示します。

次のコマンドを使用して、 [ **DevCon DriverFiles** ](devcon-driverfiles.md)操作を使用して、システム上のデバイス ドライバーのファイル名を一覧表示します。 コマンドは、使われているワイルドカード文字 (**\\* * *) をシステム上のすべてのデバイスを示すためにします。コマンドがリダイレクト文字を使用して、出力は、広範なであるため (*<em>&gt;</em>*) の参照をファイルに出力をリダイレクトする driverfiles.txt します。

```
devcon driverfiles * > driverfiles.txt
```

### <span id="ddk_example_9_list_the_driver_files_of_a_particular_device_tools"></span><span id="DDK_EXAMPLE_9_LIST_THE_DRIVER_FILES_OF_A_PARTICULAR_DEVICE_TOOLS"></span><a name="ddk_example_9_list_the_driver_files_of_a_particular_device_tools"></a>例 9:特定のデバイスのドライバー ファイルを一覧表示します。

次のコマンドを使用して、 [ **DevCon DriverFiles** ](devcon-driverfiles.md)操作がローカル コンピューターのマウス デバイスで使用されるデバイス ドライバーを検索します。 そのハードウェア Id のいずれかによって、デバイスが識別されます HID\\Vid\_045e & Pid\_0039 & Rev\_0121 します。 アンパサンド文字が含まれているために、ID が引用符で囲まれたハードウェア (**&**)。

```
devcon driverfiles "HID\Vid_045e&Pid_0039&Rev_0121"
```

応答では、DevCon はマウス デバイスをサポートする 2 つのデバイス ドライバーを表示します。

```
HID\VID_045E&PID_0039\6&DC36FDE&0&0000
    Name: Microsoft USB IntelliMouse Optical
    Driver installed from c:\windows\inf\msmouse.inf [HID_Mouse_Inst]. 2 file(s)
 used by driver:
        C:\WINDOWS\System32\DRIVERS\mouhid.sys
        C:\WINDOWS\System32\DRIVERS\mouclass.sys
1 matching device(s) found.
```

### <span id="ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools"></span><span id="DDK_EXAMPLE_10_LIST_DRIVER_PACKAGES_BY_HARDWARE_ID_PATTERN_TOOLS"></span><a name="ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools"></a>例 10:ハードウェア ID のパターンでドライバー パッケージの一覧

次のコマンドを使用して、 [ **DevCon DriverNodes** ](devcon-drivernodes.md)コマンドと ID のパターンをソフトウェアによって列挙されたデバイスのドライバー ノードを一覧表示します。 パターンは、同じセットアップ クラスにできない可能性がある類似するデバイスに関する情報を見つけるのに役立ちます。

次のコマンド ID のパターンを使用して**sw\\*** ハードウェア Id または互換性 Id を持つで始まる"sw"は、デバイスのソフトウェアで列挙されるデバイスを指定します。

```
devcon drivernodes sw*
```

応答として、DevCon システムにソフトウェアで列挙されるデバイスのドライバー ノードが表示されます。

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

### <span id="ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool"></span><span id="DDK_EXAMPLE_11_LIST_DRIVER_PACKAGES_BY_DEVICE_INSTANCE_ID_PATTERN_TOOL"></span><a name="ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool"></a>例 11:デバイス インスタンス ID のパターンでドライバー パッケージの一覧

次のコマンドを使用して、 [ **DevCon DriverNodes** ](devcon-drivernodes.md)とルートを持つデバイス インスタンス Id のすべてのデバイスのドライバー パッケージを一覧表示操作を開始\\列挙型では、デバイスのメディア\\ルート\\メディア レジストリ サブキー。 コマンドを使用して、文字 (**@**) という語句がデバイス インスタンス ID であることを示します

```
devcon drivernodes @ROOT\MEDIA*
```

応答の DevCon するには、インスタンス ID を持つデバイスが始まるデバイスのドライバー ノードが表示されます"ルート\\メディア。"。

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

### <span id="ddk_example_12_list_resources_of_a_class_of_devices_tools"></span><span id="DDK_EXAMPLE_12_LIST_RESOURCES_OF_A_CLASS_OF_DEVICES_TOOLS"></span><a name="ddk_example_12_list_resources_of_a_class_of_devices_tools"></a>12 の例:デバイスのクラスのリソースを一覧表示

次のコマンドを使用して、 [ **DevCon リソース**](devcon-resources.md) Hdc デバイス セットアップ クラス内のデバイスに割り当てられているリソースを表示する操作。 このクラスには、IDE コント ローラーが含まれています。 等号 (=) (**=**) にある、クラスと ID ではないことを示すには、"hdc"が付加されます

```
devcon resources =hdc
```

応答では、DevCon には、ローカル コンピューター上の IDE コント ローラーに割り当てられたリソースが一覧表示されます。

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

### <span id="ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too"></span><span id="DDK_EXAMPLE_13_LIST_RESOURCES_OF_DEVICE_ON_A_REMOTE_COMPUTER_BY_ID_TOO"></span><a name="ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too"></a>13 の使用例:デバイス ID でリモート コンピューター上のリソースを一覧表示

次のコマンドを使用して、 [ **DevCon リソース**](devcon-resources.md) Server01 上のシステム タイマーにリモート コンピューターに割り当てられたリソースの一覧を操作します。 コマンドは、システムのタイマー ACPI のハードウェア ID を使用して\\PNP0100、デバイスを指定します。

```
devcon /m:\\Server01 resources *PNP0100
```

応答では、DevCon は、Server01 のシステム タイマーのリソースを表示します。

```
ROOT\*PNP0100\PNPBIOS_8
    Name: System timer
    Device has the following resources reserved:
        IO  : 0040-005f
        IRQ : 0
1 matching device(s) found on \\server01.
```

次のコマンドは、DevCon リソース コマンドで、リモート システム タイマーのデバイス インスタンス ID を使用します。 文字 (**@**) 文字列がデバイス インスタンス ID、いないハードウェア ID または互換性 ID であることを示します。

```
devcon /m:\\Server01 resources @ACPI\PNP0100\4&b4063f4&0
```

### <span id="ddk_example_14_display_the_driver_stack_for_storage_devices_tools"></span><span id="DDK_EXAMPLE_14_DISPLAY_THE_DRIVER_STACK_FOR_STORAGE_DEVICES_TOOLS"></span><a name="ddk_example_14_display_the_driver_stack_for_storage_devices_tools"></a>14 の使用例:記憶装置のドライバー スタックを表示します。

次のコマンドを使用して、 [ **DevCon スタック**](devcon-stack.md)ボリューム内のデバイス セットアップ クラスとそれらのデバイスの必要なドライバー スタックの表示を検索する操作。 等号 (=) (**=**)、文字列は、クラス名であることを示します。

```
devcon stack =Volume
```

応答では、DevCon はボリューム クラス内のデバイスの予想されるスタックを表示します。 返されるデータには、デバイス インスタンス ID と GUID と、デバイス セットアップ クラスの名前、上限と下限のフィルター ドライバー、および制御するサービスの名前は、各デバイスの説明が含まれます (該当する場合)。

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

### <span id="ddk_example_15_find_the_setup_class_of_a_device_tools"></span><span id="DDK_EXAMPLE_15_FIND_THE_SETUP_CLASS_OF_A_DEVICE_TOOLS"></span><a name="ddk_example_15_find_the_setup_class_of_a_device_tools"></a>15 の使用例:デバイスのセットアップ クラスを見つける

[ **DevCon スタック**](devcon-stack.md)操作が、上限と下限のフィルター ドライバーだけでなく、デバイスのセットアップ クラスを返します。 次のコマンドでは、そのデバイス インスタンス ID を検索し、そのセットアップ クラスを検索するデバイス インスタンス ID を使用してプリンター ポートのインターフェイスのセットアップ クラスを検索します。

次のコマンドを使用して、 [ **DevCon HwIDs** ](devcon-hwids.md) "LPT、"プリンター ポートのハードウェア ID 内の句を使用して、プリンター ポート インターフェイスのデバイス インスタンス ID を検索する操作

```
devcon hwids *lpt*
```

応答では、DevCon は (太字で表示される) デバイス インスタンス ID と、プリンター ポート インターフェイスのハードウェア ID を返します。

```
LPTENUM\MICROSOFTRAWPORT\5&CA97D7E&0&LPT1
    Name: Printer Port Logical Interface
    Hardware ID's:
        LPTENUM\MicrosoftRawPort958A
        MicrosoftRawPort958A
1 matching device(s) found.
```

次のコマンドを使用して、 [ **DevCon スタック**](devcon-stack.md)デバイス インスタンス ID によって表されるデバイスのデバイス セットアップ クラスを検索する操作 文字 (**@**) デバイス インスタンス ID として ID を識別します アンパサンド文字が含まれているために、ID は引用符で囲みます。

```
devcon stack "@LPTENUM\MICROSOFTRAWPORT\5&CA97D7E&0&LPT1"
```

応答では、DevCon クラスを含む、プリンター ポート インターフェイスのドライバー スタックが表示されます。 表示するには、プリンター ポートが、システムのクラスが表示されます。

```
LPTENUM\MICROSOFTRAWPORT\5&CA97D7E&0&LPT1
    Name: Printer Port Logical Interface
    Setup Class: {4D36E97D-E325-11CE-BFC1-08002BE10318} System
    Controlling service:
        (none)
1 matching device(s) found.
```

### <span id="ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu"></span><span id="DDK_EXAMPLE_16_DISPLAY_THE_STACK_FOR_RELATED_DEVICES_ON_A_REMOTE_COMPU"></span><a name="ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu"></a>16 の使用例:リモート コンピューターに関連するデバイスの履歴を表示します。

次のコマンドを使用して、 **DevCon スタック**リモート コンピューター Server01 上のミニポート ドライバーのデバイスの操作を表示、予想されるスタックします。 「ミニポート」Net セットアップ クラスのデバイスに対して、ハードウェア ID または互換性 ID 内で検索します。

このコマンドは最初の検索に Net セットアップ クラスを限定し、「ミニポート」の文字列を検索し、注意してください。 Net セットアップ クラスのもの以外のデバイスが見つかりません。

```
devcon /m:\\server01 stack =net *miniport*
```

応答では、DevCon は、Server01 上ミニポート ドライバーに予想されるスタックを表示します。

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

### <span id="ddk_example_17_display_the_status_of_all_devices_on_the_local_computer"></span><span id="DDK_EXAMPLE_17_DISPLAY_THE_STATUS_OF_ALL_DEVICES_ON_THE_LOCAL_COMPUTER"></span><a name="ddk_example_17_display_the_status_of_all_devices_on_the_local_computer"></a>17 の使用例:ローカル コンピューターのすべてのデバイスの状態を表示します。

次のコマンドを使用して、 [ **DevCon 状態**](devcon-status.md)操作がローカル コンピューターのすべてのデバイスのステータスを確認します。 Status.txt ファイルのログ記録、またはそれ以降の状態を保存し確認します。 コマンドは、使われているワイルドカード文字 (**\\* * *) を表すすべてのデバイスとリダイレクト文字 (*<em>&gt;</em>*) status.txt ファイルに出力をリダイレクトします。

```
devcon status * > status.txt
```

### <span id="ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to"></span><span id="DDK_EXAMPLE_18_DISPLAY_THE_STATUS_OF_A_DEVICE_BY_DEVICE_INSTANCE_ID_TO"></span><a name="ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to"></a>18 の使用例:デバイス インスタンス ID の状態を表示します。

特定のデバイスの状態を確認する最も信頼性の高い方法は、デバイスのデバイス インスタンス ID を使用することです。

次のコマンドでローカル コンピューター上の I/O コント ローラー デバイス インスタンス ID を使用して、 [ **DevCon 状態**](devcon-status.md)コマンド。 コマンドには、PCI、デバイスのデバイス インスタンス ID が含まれています。\\VEN\_8086 & DEV\_1130 & SUBSYS\_00000000 & REV\_02\\3 & 29E81982 & 0 & 00 です。 文字 (**@**) プレフィックスを ID は、デバイス インスタンス ID として文字列を識別します。 アンパサンド文字が含まれているために、ID を引用符で囲む必要があります。

```
devcon status "@PCI\VEN_8086&DEV_1130&SUBSYS_00000000&REV_02\3&29E81982&0&00"
```

応答では、DevCon は I/O コント ローラーの状態を表示します。

```
PCI\VEN_8086&DEV_1130&SUBSYS_00000000&REV_02\3&29E81982&0&00
    Name: Intel(R) 82815 Processor to I/O Controller - 1130
    Driver is running.
1 matching device(s) found.
```

### <span id="ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu"></span><span id="DDK_EXAMPLE_19_DISPLAY_THE_STATUS_OF_RELATED_DEVICES_ON_A_REMOTE_COMPU"></span><a name="ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu"></a>19 の使用例:リモート コンピューターに関連するデバイスの状態を表示します。

次のコマンドを使用して、 [ **DevCon 状態**](devcon-status.md)操作を Server01 リモート コンピューター上の特定の記憶域に関連するデバイスの状態を表示します。 次のデバイスを検索します。

-   ディスク ドライブ、GenDisk

-   CD-ROM ドライブ、GenCdRom

-   フロッピー ディスク ドライブ、FDC\\ジェネリック\_フロッピー\_ドライブ

-   ボリューム、ストレージ\\ボリューム

-   論理ディスク マネージャーで、ルート\\DMIO

-   ボリューム マネージャー、ルート\\FTDISK

-   フロッピー ディスク コント ローラー、ACPI\\PNP0700

コマンドを各 ID から他のスペースで区切られています。 その他の Id は、ハードウェア Id に対して GenDisk と GenCdRom が互換性の Id に注意してください。

```
devcon /m:\\server01 status GenDisk GenCdRom FDC\GENERIC_FLOPPY_DRIVE STORAGE\Volume ROOT\DMIO ROOT\FTDISK ACPI\PNP0700
```

応答では、DevCon には、各デバイスの状態が表示されます。

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

### <span id="ddk_example_20_find_devices_by_hardware_id_pattern_tools"></span><span id="DDK_EXAMPLE_20_FIND_DEVICES_BY_HARDWARE_ID_PATTERN_TOOLS"></span><a name="ddk_example_20_find_devices_by_hardware_id_pattern_tools"></a>20 の使用例:ハードウェア ID のパターンでデバイスを検索します。

次のコマンドを使用して、 [ **DevCon 検索**](devcon-find.md)マウス デバイス、Server01 リモート コンピューターを検索する操作。 具体的には、Server01 コンピューターのハードウェア ID または互換性 ID を持つ「マウス」が含まれています。 デバイスの検索コマンド

```
devcon /m:\\Server01 find *mou*
```

この場合は、DevCon では、2 つのマウス デバイスの両方が見つかりました。

```
ROOT\*PNP0F03\1_0_21_0_31_0                                 : Microsoft PS/2 Mouse
ROOT\RDP_MOU\0000                                           : Terminal Server Mouse Driver
```

DevCon ディスプレイのすべての操作は、ハードウェア Id を検索するも、ためには、ハードウェア Id を検索する任意の表示操作を使用できます。 出力で必要な内容に基づく操作を選択します。 たとえば、デバイス ドライバーを検索するそのマウス関連のデバイスで、ローカル コンピューターを使用するには、次のコマンドを送信します。

```
devcon driverfiles *mou*
```

応答では、DevCon は、デバイスを検索し、そのドライバーを一覧表示します。

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

### <span id="ddk_example_21_find_devices_by_device_instance_id_or_class_tools"></span><span id="DDK_EXAMPLE_21_FIND_DEVICES_BY_DEVICE_INSTANCE_ID_OR_CLASS_TOOLS"></span><a name="ddk_example_21_find_devices_by_device_instance_id_or_class_tools"></a>21 の使用例:デバイス インスタンス ID またはクラスによってデバイスを検索します。

使用して、次のコマンド、 [ **DevCon 検索**](devcon-find.md)操作をローカル コンピューターのすべてのレガシ デバイスを表示します。 検索する必要がある従来のデバイスは、ハードウェア ID を持っていないために、デバイス インスタンス ID (レジストリ パス) では、ルート\\レガシ、またはセットアップ クラス、LegacyDriver します。

最初のコマンドは、デバイス インスタンス ID パターンによって、従来のドライバーを検索します。 前に、ID のパターンは、文字で (**@**) デバイス インスタンス ID を示すワイルドカード文字が続くと (* *\\* * *) ルートですべてのデバイスを検索する\\レガシ サブキー。

```
devcon find @root\legacy*
```

2 番目のコマンドは、LegacyDriver クラスのすべてのデバイスを検索して、従来のデバイスを検索します。

```
devcon find =legacydriver
```

どちらのコマンドの出力は同じ、ここでは、同じ 27 従来のデバイスを検索します。

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

### <span id="ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools"></span><span id="DDK_EXAMPLE_22_FIND_AND_FIND_ALL_DEVICES_IN_A_SETUP_CLASS_TOOLS"></span><a name="ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools"></a>22 の使用例:検索 (および すべて検索) デバイス セットアップ クラス

次のコマンドを使用して、 [ **DevCon FindAll** ](devcon-findall.md) Net セットアップ クラスのコンピューター上のすべてのデバイスを検索する操作。 等号 (=) (**=**) Net がセットアップ クラスと ID ではないことを示します

```
devcon findall =net
```

応答では、DevCon には、Net セットアップ クラスの次の 7 つのデバイスが一覧表示します。 最初の 6 つは、標準のミニポート ドライバーのデバイスです。 7 番目のデバイスでは、RAS 非同期アダプターは、ソフトウェア列挙デバイス (SW\\\*) が必要になるまでにインストールされていないいます。

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

次のコマンドを比較し、 [ **DevCon 検索**](devcon-find.md)と**DevCon FindAll**操作を実行して、 **DevCon 検索**コマンドと同じパラメーターが前**DevCon FindAll**コマンド。

```
devcon find =net
```

応答では、DevCon には、Net セットアップ クラスの次の 6 つのデバイスが一覧表示します。

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

予測的に、 **DevCon 検索**デバイスがインストールされていないために、コマンドで、現在インストールされているデバイスのみを返しますはソフトウェアで列挙されるデバイスの一覧を表示できません。

### <span id="ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools"></span><span id="DDK_EXAMPLE_23_DISPLAY_THE_FILTER_DRIVERS_FOR_A_SETUP_CLASS_TOOLS"></span><a name="ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools"></a>23 の使用例:セットアップ クラスに対するドライバーだけを表示します。

次のコマンドを使用して、 [ **DevCon ClassFilter** ](devcon-classfilter.md)操作をディスク ドライブのセットアップ クラスの上部のフィルター ドライバーを表示します。 このコマンドに classfilter 演算子が含まれていないため、DevCon はクラスのフィルター ドライバーが表示されますが、それらは変わりません。

```
devcon classfilter DiskDrive upper
```

応答として、DevCon はディスク ドライブのクラスの上位のフィルター ドライバーが表示され、変更されていないことを確認します。 この場合、デバイス セットアップ クラスが、ディスク ドライブが PartMgr.sys 上位フィルター ドライバーを使用することが表示されます。

```
Class filters unchanged.
    PartMgr
```

### <span id="ddk_example_24_add_a_filter_driver_to_a_setup_class_tools"></span><span id="DDK_EXAMPLE_24_ADD_A_FILTER_DRIVER_TO_A_SETUP_CLASS_TOOLS"></span><a name="ddk_example_24_add_a_filter_driver_to_a_setup_class_tools"></a>24 の使用例:フィルター ドライバー セットアップ クラスを追加します。

次のコマンドを使用して、 [ **DevCon ClassFilter** ](devcon-classfilter.md) Disklog.sys、架空のフィルターをディスク ドライブのセットアップ クラスの上部のフィルター ドライバーの一覧に追加する操作。

このコマンドは、追加後は使用して (**+**) ClassFilter 演算子 PartMgr.sys が既に処理されたデータを受信するように PartMgr ドライバーの後に Disklog ドライバーをロードします。

コマンドの開始時に、仮想カーソルが最初のフィルター ドライバーの前に配置されます。 特定のドライバーには配置されません、ため DevCon フィルター ドライバーの一覧の末尾に Disklog ドライバーを追加します。

コマンドを使用しても、 **/r**パラメーターで、変更、クラス フィルターを有効にする必要がある場合、システムを再起動します。

```
devcon /r classfilter DiskDrive upper +Disklog
```

応答では、DevCon には、ディスク ドライブのクラスの現在の上位フィルター ドライバーが表示されます。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    Disklog
```

ドライバ名のスペルを入力するか、またはシステムにインストールされていないドライバーを追加しようとする場合、コマンドは失敗します。 DevCon は追加されません、ドライバー、ドライバーは、サービスとしては、登録されていない限り、ドライバーでは、サービスのレジストリ サブキーにサブキーが含まれている場合を除き、(HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス)。

次のコマンドは、この保護機能をテストします。 ("Disklog") ではなく"Disklgg"を追加するディスク ドライブ クラス上部のフィルターの一覧を試みます。 出力は、コマンドが失敗したことを示します。

```
devcon /r classfilter DiskDrive upper +Disklgg
devcon failed.
```

### <span id="ddk_example_25_insert_a_filter_driver_in_the_class_list_tools"></span><span id="DDK_EXAMPLE_25_INSERT_A_FILTER_DRIVER_IN_THE_CLASS_LIST_TOOLS"></span><a name="ddk_example_25_insert_a_filter_driver_in_the_class_list_tools"></a>25 の使用例:[クラス] 一覧で、フィルター ドライバーを挿入します。

次のコマンドを使用して、 [ **DevCon ClassFilter** ](devcon-classfilter.md) MyFilter.sys、架空のフィルター ドライバーをディスク ドライブのセットアップ クラスの上部のフィルター ドライバーの一覧に追加する操作。 コマンドは、負荷の順序で PartMgr.sys と Disklog.sys 間 MyFilter.sys を配置します。

```
devcon /r classfilter DiskDrive upper @Disklog -MyFilter
```

次の一覧は、コマンドが送信される前に、ディスク ドライブのクラスのフィルター ドライバーを示します。

```
    PartMgr
    Disklog
```

最初のサブコマンド<strong>@Disklog</strong>、配置の演算子を使用して (**@**) Disklog フィルター ドライバーに仮想のカーソルを配置します。 2 つ目のサブコマンド **- MyFilter**、追加の使用-演算子の前に (**-**) MyFilter.sys Disklog.sys する前に追加します。

コマンドを使用しても、 **/r**パラメーターで、変更、クラス フィルターを有効にする必要がある場合、システムを再起動します。

配置の演算子は、この例では不可欠です。 DevCon 任意 classfilter サブコマンドを処理する前に仮想のカーソルは、リストの先頭にあるし、すべてのフィルター ドライバーに配置されていません。 追加を使用する場合の前に (**+**) ドライバーに配置されているカーソルに含まれていない場合、演算子、DevCon がリストの先頭に、ドライバーを追加します。 追加後に使用する場合 (**-**) 演算子のドライバーに対して、カーソルが位置していない場合、リストの末尾にドライバーを追加します。

応答では、DevCon には、ディスク ドライブのクラスの現在の上位フィルター ドライバーが表示されます。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    MyFilter
    Disklog
```

MyFilter ドライバーを追加して、PartMgr と Disklog の間に、次のコマンドを使用することもできます。 この例では、最初のサブコマンドで<strong>@PartMgr</strong>、PartMgr フィルター ドライバーに仮想のカーソルを位置付けます。 2 番目のサブコマンド **+ MyFilter**、PartMgr MyFilter.sys を追加する追加後演算子 (+) を使用します。

```
devcon /r classfilter DiskDrive upper @PartMgr +MyFilter
```

### <span id="ddk_example_26_replace_a_filter_driver_tools"></span><span id="DDK_EXAMPLE_26_REPLACE_A_FILTER_DRIVER_TOOLS"></span><a name="ddk_example_26_replace_a_filter_driver_tools"></a>26 の使用例:フィルター ドライバーを置き換える

次のコマンドを使用して、 [ **DevCon ClassFilter** ](devcon-classfilter.md) MyFilter.sys の元のコピーをバージョンに置き換える、新規および改良された、MyNewFilter.sys のフィルター ドライバーの一覧で、操作、ディスク ドライブのセットアップ クラスです。

```
devcon /r classfilter DiskDrive upper !MyFilter +MyNewFilter
```

次の一覧は、コマンドが送信される前に、ディスク ドライブのクラスのフィルター ドライバーを示します。

```
    PartMgr
    MyFilter
    Disklog
```

最初のサブコマンドが delete 演算子を使用して (**!**) MyFilter をディスク ドライブのクラスの上部のフィルター ドライバーの一覧から削除します。 (C: MyFilter.sys ファイルには影響しません\\Windows\\System32\\ドライバー ディレクトリ)。

2 番目のサブコマンドは、追加後に演算子を使用して (**+**) 削除されたドライバーが占有される位置に、新しいフィルター ドライバーを配置します。 Delete 演算子のまま、カーソルの位置にあるため、削除されたフィルター占有されている、追加の前に (**-**) と追加した後 (**+**) 演算子と同じ効果があります)。

コマンドを使用しても、 **/r**パラメーターで、変更、クラス フィルターを有効にする必要がある場合、システムを再起動します。

応答では、DevCon はディスク ドライブのクラスの新しいクラス フィルターの構成を示します。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    MyNewFilter
    Disklog
```

### <span id="ddk_example_27_change_the_order_of_filter_drivers_tools"></span><span id="DDK_EXAMPLE_27_CHANGE_THE_ORDER_OF_FILTER_DRIVERS_TOOLS"></span><a name="ddk_example_27_change_the_order_of_filter_drivers_tools"></a>27 の使用例:フィルター ドライバーの順序を変更します。

次のコマンドを使用して、 [ **DevCon ClassFilter** ](devcon-classfilter.md)セットアップ クラスが、ディスク ドライブのフィルター ドライバーの順序を変更する操作。 具体的には、2 番目と 3 番目のフィルター ドライバーの順序を反転させます。

```
devcon /r classfilter DiskDrive upper !Disklog =@PartMgr +Disklog
```

次の一覧は、コマンドが送信される前に、ディスク ドライブのクラスのフィルター ドライバーを示します。 コマンドの意図した結果も表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">変更前</th>
<th align="left">クリック後</th>
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

 

最初のサブコマンドが delete 演算子を使用して (**!)** Disklog を一覧から削除します。 2 番目のサブコマンドがスタート演算子を使用して (**=)** に仮想のカーソルを開始位置に移動し、配置の演算子を使用して (**@)** PartMgr ドライバーにカーソルを配置します。 開始演算子は、仮想のカーソルがリストを順方向にのみ移動するために必要があります。 最後のサブコマンドは、追加後に演算子を使用して (**+)** PartMgr 後 Disklog を追加します。

応答では、DevCon はディスク ドライブのクラスの新しいクラス フィルターの構成を示します。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    Disklog
    MyNewFilter
```

### <span id="ddk_example_28_enable_a_particular_device_tools"></span><span id="DDK_EXAMPLE_28_ENABLE_A_PARTICULAR_DEVICE_TOOLS"></span><a name="ddk_example_28_enable_a_particular_device_tools"></a>28 の使用例:特定のデバイスを有効にします。

次のコマンドを使用して、 [ **DevCon 有効**](devcon-enable.md)システムの問題の修正を無効化されていた programmable interrupt controller を有効にする操作。 ため、コント ローラーのハードウェア ID \*PNP0000 にアスタリスクが含まれています、コマンドは、単一引用符を使用して (**'**) コマンドで指定されているのとまったく同様に、ハードウェア ID を検索する DevCon に出力するためです。 それ以外の場合、アスタリスクをワイルドカード文字として解釈は。

```
devcon enable '*PNP0000
```

応答では、DevCon は、デバイスのデバイス インスタンス ID が表示され、デバイスを有効にするシステムを再起動する必要がありますを説明します。

```
ACPI\PNP0000\4&B4063F4&0                                    : Enabled on reboot
Not all of 1 device(s) enabled, at least one requires reboot to complete the operation.
```

またはを使用して、システムのいずれか、手動で再起動して応答することができます、 [ **DevCon 再起動**](devcon-reboot.md)操作。

次のコマンドを追加、 **/r**前のコマンド パラメーター。 **/R**操作を完了する必要が再起動する場合にのみ、パラメーターは、システムを再起動します。

```
devcon /r enable '*PNP0000
```

応答として、DevCon は、デバイスし、有効化を有効にするシステムを再起動します。

システムの起動時には、DevCon 状態のコマンドを使用して、デバイスが有効になっていることを確認します。

```
devcon status '*PNP0000

ACPI\PNP0000\4&B4063F4&0
    Name: Programmable interrupt controller
    Driver is running.
```

### <span id="ddk_example_29_enable_devices_by_class_tools"></span><span id="DDK_EXAMPLE_29_ENABLE_DEVICES_BY_CLASS_TOOLS"></span><a name="ddk_example_29_enable_devices_by_class_tools"></a>29 の使用例:クラスによってデバイスを有効にします。

次のコマンドでプリンター セットアップ クラスを指定することで、コンピューター上のすべてのプリンター デバイスの有効な[ **DevCon 有効にする**](devcon-enable.md)コマンド。 コマンドが含まれています、 **/r**パラメーターで、有効化を有効にする必要がある場合、システムを再起動します。

```
devcon /r enable =Printer
```

応答では、DevCon のプリンター、プリンターのクラスが有効になっているレポートで検出されたデバイス インスタンス ID が表示されます。 含まれていますが、コマンド、 **/r**パラメーター、プリンターを有効にするには再起動が必要ではないために、システムは再起動されませんでした。

```
LPTENUM\HEWLETT-PACKARDDESKJET_1120C\1&7530F08&0&LPT1.4        : Enabled
1 device(s) enabled.
```

### <span id="ddk_example_30_disable_devices_by_an_id_pattern_tools"></span><span id="DDK_EXAMPLE_30_DISABLE_DEVICES_BY_AN_ID_PATTERN_TOOLS"></span><a name="ddk_example_30_disable_devices_by_an_id_pattern_tools"></a>30 の使用例:ID、パターンによってデバイスを無効にします。

次のコマンドを使用して、 [ **DevCon 無効**](devcon-disable.md)ローカル コンピューター上の USB デバイスを無効にする操作。 ハードウェア ID のパターンによって、デバイスが特定 (USB\*)。 このパターンでのハードウェア ID または互換性 ID が"USB"で始まる任意のデバイスが一致します。 コマンドが含まれています、 **/r**パラメーターで、無効化を有効にする必要がある場合、システムを再起動します。

**注**デバイスを無効にする、ID のパターンを使用する前に、影響を受けるデバイスを決定します。 表示コマンドで使用してパターンをなどを行うに**devcon 状態 USB\\*** または * * devcon hwids USB\\* * *。

 

```
devcon /r disable USB*
```

応答では、DevCon は USB デバイスのデバイス インスタンス Id が表示し、無効になっているを報告します。 含まれていますが、コマンド、 **/r**パラメーター、デバイスを無効にするには再起動が必要ではないために、システムは再起動されませんでした。

```
USB\ROOT_HUB\4&2A40B465&0
: Disabled
USB\ROOT_HUB\4&7EFA360&0
: Disabled
USB\VID_045E&PID_0039\5&29F428A4&0&2
: Disabled
3 device(s) disabled.
```

### <span id="ddk_example_31_disable_devices_by_device_instance_id_tools"></span><span id="DDK_EXAMPLE_31_DISABLE_DEVICES_BY_DEVICE_INSTANCE_ID_TOOLS"></span><a name="ddk_example_31_disable_devices_by_device_instance_id_tools"></a>31 の使用例:デバイス インスタンス ID でデバイスを無効にします。

次のコマンドを使用して、 [ **DevCon 無効**](devcon-disable.md)ローカル コンピューター上の USB デバイスを無効にする操作。 このコマンドで示されているデバイス インスタンス Id によって、デバイスを特定の文字で (**@**) 前になる各 ID 各デバイス インスタンス ID は、スペースで他の区切られています。

また、デバイス インスタンス Id はアンパサンド文字を含めるため (**&**)、引用符で囲みます。 コマンドが含まれています、 **/r**パラメーターで、無効化を有効にする必要がある場合、システムを再起動します。

```
devcon /r disable "@USB\ROOT_HUB\4&2A40B465&0" "@USB\ROOT_HUB\4&7EFA360&0" "@USB\VID_045E&PID_0039\5&29F428A4&0&2"
```

応答では、DevCon は USB デバイスのデバイス インスタンス Id が表示し、無効になっているを報告します。 含まれていますが、コマンド、 **/r**パラメーター、デバイスを無効にするには再起動が必要ではないために、システムは再起動されませんでした。

```
USB\ROOT_HUB\4&2A40B465&0
: Disabled
USB\ROOT_HUB\4&7EFA360&0
: Disabled
USB\VID_045E&PID_0039\5&29F428A4&0&2
: Disabled
3 device(s) disabled.
```

### <span id="ddk_example_32_update_the_driver_for_communication_ports_tools"></span><span id="DDK_EXAMPLE_32_UPDATE_THE_DRIVER_FOR_COMMUNICATION_PORTS_TOOLS"></span><a name="ddk_example_32_update_the_driver_for_communication_ports_tools"></a>例: 32:通信ポートのドライバーを更新します。

次のコマンドを使用して、 [ **DevCon 更新**](devcon-update.md) test.inf ファイルで指定されたテスト ドライバーを使用した、システムの通信ポートの現在のデバイス ドライバーを置換する操作。 コマンドは、全体のハードウェア id を持つデバイスのみに影響\*PNP0501 (アスタリスクを含む)。

システムで署名されたドライバーを置き換える代替のドライバーのテストやトラブルシューティング、または同じドライバーの最新のバージョンと、デバイスを関連付けるには、このコマンドを使用できます。

```
devcon update c:\windows\inf\test.inf *PNP0501
```

応答 DevCon 表示、**ハードウェアの設置**警告は、ドライバーで Windows のロゴ テスト渡さないことについて説明します。 クリックすると、**続行とにかく**ダイアログ ボックスのボタンでは、インストールが続行されます。

次に、DevCon には、次の成功メッセージが表示されます。

```
Updating drivers for *PNP0501 from c:\windows\inf\test.inf.
Drivers updated successfully.
```

使用することも、 [ **DevCon UpdateNI** ](devcon-updateni.md)操作、非対話型のバージョン、 **DevCon 更新**ドライバーの更新の操作。 **DevCon UpdateNI**操作のと同じですが、 **DevCon 更新**こと以外の操作の応答を必要とするすべてのユーザー メッセージを非表示にし、プロンプトに既定の応答を前提としています。

次のコマンドを使用して、 **DevCon UpdateNI**テスト ドライバーをインストールする操作。

```
devcon updateni c:\windows\inf\test.inf *PNP0501
```

この場合は、DevCon は表示されない、**ハードウェアの設置**警告します。 代わりに、既定の応答と想定して**停止インストール**します。 その結果、DevCon はドライバーを更新することはできませんし、エラー メッセージを表示します。

```
Updating drivers for *PNP0501 from c:\windows\inf\test.inf.
devcon failed.
```

### <span id="ddk_example_33_install_a_device_tools"></span><span id="DDK_EXAMPLE_33_INSTALL_A_DEVICE_TOOLS"></span><a name="ddk_example_33_install_a_device_tools"></a>33 の使用例:デバイスをインストールします。

次のコマンドを使用して、 [ **DevCon インストール**](devcon-install.md)操作がローカル コンピューターのキーボード デバイスをインストールします。 コマンドには、デバイス (keyboard.inf) およびハードウェア ID の INF ファイルへの完全パスが含まれています (\*PNP030b)。

```
devcon /r install c:\windows\inf\keyboard.inf *PNP030b
```

応答には、インストールされているデバイスは、新しいデバイスのデバイス ノードの作成が、デバイスのドライバー ファイルが更新され、DevCon に報告します。

```
Device node created. Install is complete when drivers files are updated...
Updating drivers for *PNPO30b from c:\windows\inf\keyboard.inf
Drivers updated successfully.
```

### <span id="ddk_example_34_install_a_device_using_unattended_setup_tools"></span><span id="DDK_EXAMPLE_34_INSTALL_A_DEVICE_USING_UNATTENDED_SETUP_TOOLS"></span><a name="ddk_example_34_install_a_device_using_unattended_setup_tools"></a>34 の使用例:無人セットアップを使用してデバイスをインストールします。

次の例では、Microsoft Windows XP の無人インストール中に Microsoft Loopback Adapter をインストールする方法を示します。

無人セットアップ中にこのデバイスをインストールする、次のファイルをフロッピー ディスクに追加することで開始: devcon.exe と netloop.inf (c:\\Windows\\inf\\netloop.inf)。

次に、 **\[GUIRunOnce\]** セクションの無人セットアップ ファイルには、次の DevCon コマンドを追加します。

```
a:\devcon /r install a:\Netloop.inf '*MSLOOP
```

このコマンドは、ハードウェア ID を使用して、ループバック アダプターを識別する\*MSLOOP します。 上記の単一引用符文字"\*MSLOOP"DevCon は文字どおり、文字列を解釈する、ワイルドカード文字としてではなく、ハードウェア ID の一部としてアスタリスクを解釈するように指示します。

コマンドには、インストールで DevCon を使用する (フロッピー ディスク) 上に Netloop.inf ファイルも指定します。 **/R**パラメーターが、再起動がインストールを完了するために必要な場合にのみ、コンピューターを再起動します。

最後に、無人セットアップ ファイルをネットワーク構成設定を追加し、無人セットアップを実行します。

### <span id="ddk_example_35_remove_devices_by_device_instance_id_pattern_tools"></span><span id="DDK_EXAMPLE_35_REMOVE_DEVICES_BY_DEVICE_INSTANCE_ID_PATTERN_TOOLS"></span><a name="ddk_example_35_remove_devices_by_device_instance_id_pattern_tools"></a>35 の使用例:デバイス インスタンス ID のパターンによってデバイスを削除します。

次のコマンドを使用して、 [ **DevCon 削除**](devcon-remove.md)をコンピューターからすべての USB デバイスを削除する操作。 始まる任意デバイス インスタンス ID (レジストリ パス) と一致するデバイス インスタンス ID パターンによって、デバイスが特定の"USB\\"文字列。 文字 (**@**) ハードウェア ID または互換性 ID とデバイスのインスタンス ID を区別 コマンドにも含まれています、 **/r**削除プロシージャを有効にすることが必要な場合は、システムを再起動するパラメーター。

**警告**パターンを使用してすべてのデバイスを削除する前にどのデバイスに影響を判断します。 表示コマンドで使用してパターンをなどを行うに<strong>devcon 状態@usb \\ \</strong > * または<strong>devcon hwids @usb \\ \</strong > *。

 

```
devcon /r remove @usb\*
```

応答では、DevCon には、これを削除するデバイスのデバイス インスタンス ID が表示されます。

```
USB\ROOT_HUB\4&2A40B465&0                             : Removed
USB\ROOT_HUB\4&7EFA360&0                              : Removed
USB\VID_045E&PID_0039\5&29F428A4&0&2                  : Removed
3 device(s) removed.
```

### <span id="ddk_example_36_remove_a_particular_network_device_tools"></span><span id="DDK_EXAMPLE_36_REMOVE_A_PARTICULAR_NETWORK_DEVICE_TOOLS"></span><a name="ddk_example_36_remove_a_particular_network_device_tools"></a>36 の使用例:特定のネットワーク デバイスを削除します。

次のコマンドを使用して、 [ **DevCon 削除**](devcon-remove.md) NDISWAN ミニポート ドライバーをローカル コンピューターからアンインストールする操作。 コマンドは、Net クラスを指定し、"ndiswan"を含めるハードウェア ID または互換性 ID を持つクラスでデバイスを指定することで、検索を制限 コマンドにも含まれています、 **/r**パラメーターで、再起動、削除の手順を有効にする必要がある場合、システムを再起動します。

**警告**パターンを使用してすべてのデバイスを削除する前に、影響を受けるデバイスを決定します。 表示コマンドで使用してパターンをなどを行うに**devcon 状態 = net \*ndiswan\\*** または * * devcon hwids = net \*ndiswan\\* * *。

 

```
devcon /r remove =net *ndiswan*
```

応答では、DevCon には、これを削除するデバイスのデバイス インスタンス ID が表示されます。

```
ROOT\MS_NDISWANIP\0000 : Removed 1 device(s) removed.
```

### <span id="ddk_example_37_scan_the_computer_for_new_devices_tools"></span><span id="DDK_EXAMPLE_37_SCAN_THE_COMPUTER_FOR_NEW_DEVICES_TOOLS"></span><a name="ddk_example_37_scan_the_computer_for_new_devices_tools"></a>37 の使用例:新しいデバイスには、コンピューターをスキャンします。

次のコマンドを使用して、 [ **DevCon を再スキャン**](devcon-rescan.md)操作がローカル コンピューターの新しいデバイスをスキャンします。

```
devcon rescan
```

システムがスキャンされることが DevCon 応答、レポートしますが、新しいデバイスが見つかりません。

```
Scanning for new hardware.
Scanning completed.
```

使用することも、 **DevCon を再スキャン**コマンドをリモート コンピューター。 次のコマンドを実行、 **DevCon を再スキャン**、Server01 上の操作を追加して、リモートのコンピューター、 **/m**パラメーターをコマンド。

```
devcon /m:\\server01 rescan
```

### <span id="ddk_example_38_restart_a_device_tools"></span><span id="DDK_EXAMPLE_38_RESTART_A_DEVICE_TOOLS"></span><a name="ddk_example_38_restart_a_device_tools"></a>38 の使用例:デバイスを再起動します。

次のコマンドを使用して、 [ **DevCon 再起動**](devcon-restart.md)ループバック アダプターは、ローカル コンピューターを再起動する操作。 デバイス インスタンス ID、ループバック アダプターのコマンドは、Net セットアップ クラスと、そのクラス内の検索の制限を指定します**ルート\\\*MSLOOP\\0000**します。 文字 (**@**) デバイス インスタンス ID として文字列を識別します。 単一引用符文字 (**'**)、DevCon がアスタリスクをワイルドカード文字として ID を解釈するを防ぎますリテラル検索では、どの要求。

```
devcon restart =net @'ROOT\*MSLOOP\0000
```

応答では、DevCon はデバイスのデバイス インスタンス ID が表示され、結果を報告します。

```
ROOT\*MSLOOP\0000                                              : Restarted
1 device(s) restarted.
```

### <span id="ddk_example_39_reboot_the_local_computer_tools"></span><span id="DDK_EXAMPLE_39_REBOOT_THE_LOCAL_COMPUTER_TOOLS"></span><a name="ddk_example_39_reboot_the_local_computer_tools"></a>39 の使用例:ローカル コンピューターを再起動します。

次のコマンドを使用して、 [ **DevCon 再起動**](devcon-reboot.md)操作がローカル コンピューターのオペレーティング システムを再起動して、ハードウェアのインストールと再起動を関連付ける。 異なり、 **/r**パラメーター、 **DevCon 再起動**操作が別の操作からのリターン コードに依存しません。

スクリプトおよびシステムの再起動を必要とするバッチ ファイルでは、このコマンドを含めることができます。

```
devcon reboot
```

応答では、DevCon には、コンピューター (ローカル コンピューターの再起動) を再起動することを示すメッセージが表示されます。


DevCon 標準を使用して**ExitWindowsEx**を再起動する関数。 ユーザーがコンピューター上の開いているファイルまたはプログラムが閉じられません、システムが、ユーザーがファイルを閉じるかプロセスを終了するシステムのプロンプトに応答するまで再起動しません。

### <span id="ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools"></span><span id="DDK_EXAMPLE_40_ASSIGN_A_HARDWARE_ID_TO_A_LEGACY_DEVICE_TOOLS"></span><a name="ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools"></a>40 の使用例:レガシ デバイスのハードウェア ID を割り当てる

次のコマンドを使用して、 [ **DevCon SetHwID** ](devcon-sethwid.md)に、ハードウェア ID を割り当てる操作ビープ音をレガシ デバイスにビープ音がします。

コマンドは、ルート、デバイスのデバイス インスタンス ID を使用して\\レガシ\_ビープ音を鳴らす\\0000、ビープ音のレガシ デバイスのハードウェア Id または互換性 Id があるないためです。 使用して、文字 (**@**)、文字列がデバイス インスタンス ID であることを示します

コマンドは、ID を配置するのに任意のシンボル パラメーターを使用しません 既定では、DevCon は、ハードウェア ID のリストの末尾に新しいハードウェア Id を追加します。 この場合、デバイスが他のハードウェア Id を持たないため、配置は関係ありません。

```
devcon sethwid @ROOT\LEGACY_BEEP\0000 := beep
```

応答では、DevCon には、デバイスのハードウェア ID の一覧にビープ音を追加、ことを示すメッセージが表示されます。 結果として得られるハードウェア ID のリストも表示されます。 この場合は、一覧には 1 つだけのハードウェア ID があります。

```
ROOT\LEGACY_BEEP\0000                              : beep
Modified 1 hardware ID(s).
```

### <span id="ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com"></span><span id="DDK_EXAMPLE_41_ADD_A_HARDWARE_ID_TO_ALL_LEGACY_DEVICES_ON_A_REMOTE_COM"></span><a name="ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com"></a>41 の使用例:リモート コンピューター上のすべてのレガシ デバイスにハードウェア ID を追加します。

次のコマンドを使用して、 [ **DevCon SetHwID** ](devcon-sethwid.md)ハードウェア ID を追加する操作、Server1 のリモート コンピューター上のすべてのレガシ デバイスのハードウェア Id の一覧には、レガシします。

コマンドを使用して、 **-** シンボル パラメーターは、デバイスのいずれかの推奨されるハードウェア ID が作成された場合に、デバイスのハードウェア ID のリストの末尾に、新しいハードウェア ID を追加します。 使用して、 **/m**パラメーターをリモート コンピューターを指定します。 デバイス インスタンス ID のパターンを使用して<strong> @ROOT\\レガシ\</strong ><em>コンピューター デバイス インスタンス ID を持つが始まるすべてのデバイスは、従来のデバイスを識別するために、**ルート\\レガシ</em>* します。

```
devcon /m:\\Server1 sethwid @ROOT\LEGACY* := -legacy
```

応答では、DevCon は影響を受けるすべてのデバイスの結果として得られるハードウェア ID の一覧を表示します。

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

デバイスのグループに同じハードウェア ID を割り当てた後は、表示および変更する 1 つのコマンド内のデバイスに、その他の DevCon 操作を使用できます。

たとえば、次のコマンドでは、すべてのレガシ デバイスの状態が表示されます。

```
devcon status legacy
```

### <span id="ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot"></span><span id="DDK_EXAMPLE_42_DELETE_A_HARDWARE_ID_FROM_ALL_LEGACY_DEVICES_ON_A_REMOT"></span><a name="ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot"></a>42 の使用例:リモート コンピューター上のすべてのレガシ デバイスからのハードウェア ID を削除します。

次のコマンドを使用して、 [ **DevCon SetHwID** ](devcon-sethwid.md) 、ハードウェア ID を削除する操作**レガシ**Server1 のリモコンのすべてのレガシ デバイスのハードウェア Id の一覧からコンピューター。

コマンドを使用して、 **/m**パラメーターをリモート コンピューターを指定します。 ハードウェア ID を使用して**レガシ**、そのハードウェア ID を持つすべてのデバイスを識別するには 次を使用して、 **!** シンボルのパラメーターを削除する、**レガシ**ハードウェア ID

```
devcon /m:\\Server1 sethwid legacy := !legacy
```

応答では、DevCon は影響を受けるすべてのデバイスの結果として得られるハードウェア ID の一覧を表示します。

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

### <span id="ddk_example_43_add_delete_and_replace_hardwareids_tools"></span><span id="DDK_EXAMPLE_43_ADD_DELETE_AND_REPLACE_HARDWAREIDS_TOOLS"></span><a name="ddk_example_43_add_delete_and_replace_hardwareids_tools"></a>43 の使用例:追加、削除、およびハードウェア Id を置き換えます

次の一連の例のさまざまな機能を使用する方法を示しています、 [ **DevCon SetHwID** ](devcon-sethwid.md)操作。

デバイス インスタンス ID を持つこの系列で使用する架空のデバイス、DeviceX、**ルート\\DeviceX\\0000**します。 DevCon を使用する前に、デバイスは次のハードウェア Id の一覧がありました。

```
Hw3 Hw4
```

次のコマンドを使用して、 **+** を追加する記号**Hw1**と**Hw2** DeviceX のハードウェア Id の一覧の先頭にします。 **Hw2**が既に表示されて、ボックスの一覧で、移動すると、追加されません。 示されているコマンドがそのデバイス インスタンス ID を使用してデバイスを識別する、文字で (**@**) 前に、id。

```
devcon sethwid @ROOT\DEVICEX\0000 := +Hw1 Hw2
```

応答では、DevCon は、デバイスの新しいハードウェア ID のリストを表示します。 なお**Hw1**と**Hw2**指定した順序でリストの先頭に表示されます。

```
ROOT\DEVICEX\0000                         : Hw1,Hw2,Hw3,Hw4
Modified 1 hardware ID(s).
```

また、DevCon は 1 つのハードウェア ID の一覧、1 つのデバイスのハードウェア ID の一覧を変更することを報告します。

次のコマンドを使用して、 **!** 削除するシンボル、 **Hw1**ハードウェア ID ハードウェア ID では、次に、表示**Hw5**シンボルのパラメーターがない場合。 シンボルのパラメーターを指定せず、SetHwID は、デバイスのハードウェア ID のリストの末尾に、ハードウェア ID を追加します。

他のシンボルのパラメーターとは異なり、このコマンドを示して、 **DevCon SetHwID**操作、 **!** シンボルは、プレフィックス、ハードウェア ID にのみ適用されます。

```
devcon sethwid @ROOT\DeviceX\0000 := !Hw1 Hw5
```

応答として、DevCon DeviceX の結果として得られるハードウェア ID のリストが表示されます。

```
ROOT\DEVICEX\0000                         : Hw2,Hw3,Hw4,Hw5
Modified 1 hardware ID(s).
```

次のコマンドを使用して、1 つのハードウェア ID を持つ DeviceX を一覧内のすべてのハードウェア Id を置き換えるパラメーターを = **DevX**します。

```
devcon sethwid @ROOT\DeviceX\0000 := =DevX
```

応答として、DevCon DeviceX の結果として得られるハードウェア ID のリストが表示されます。

```
ROOT\DEVICEX\0000                         : DevX
Modified 1 hardware ID(s).
```

成功のメッセージは、DevCon が 1 つのデバイスのハードウェア ID を変更することを示します。

### <span id="ddk_example_44_forcibly_update_the_hal_tools"></span><span id="DDK_EXAMPLE_44_FORCIBLY_UPDATE_THE_HAL_TOOLS"></span><a name="ddk_example_44_forcibly_update_the_hal_tools"></a>例 44:HAL を強制的に更新します。

次の例では、DevCon を使用して、コンピューターの HAL を更新する方法を示します。 この例では、テスト担当者はテスト目的でマルチプロセッサ APCI APIC HAL を使用してコンピューターに最適な APCI APIC HAL が適していますユニプロセッサを置換するがします。

最初のコマンドを使用して、 [ **DevCon SetHwID** ](devcon-sethwid.md)から HAL のハードウェア ID を変更する操作**acpiapic\_を**、ユニプロセッサ Hal のハードウェア ID**acpiapic\_mp**、マルチプロセッサ Hal のハードウェア ID。

ユニプロセッサおよびマルチプロセッサ Hal の両方用のドライバーが、HAL の INF ファイルに含まれているため、ハードウェア ID を変更する必要があります。 システムでは、デバイスのハードウェア ID に基づいて、INF ファイルから最も適切なドライバーを選択します。 ハードウェア ID を変更しない場合、 **DevCon 更新**コマンドは、ユニプロセッサ HAL ドライバーを再インストールだけです。

次のコマンドで、コマンドがそのインスタンス ID を使用して HAL を識別**ルート\\ACPI\_HAL\\0000**によって示されるように、 **@** ID の直前の文字 コマンドを使用して、 **+** 文字**acpiapic\_mp** HAL の一覧で最初のハードウェア ID。 次を使用して、 **!** 削除する文字、 **acpiapic\_を**HAL の Id のリストからのハードウェア ID。

```
devcon sethwid @ROOT\ACPI_HAL\0000 := +acpiapic_mp !acpiapic_up
```

応答として、DevCon HAL の次の新しいハードウェア ID の一覧が表示されます。

```
ROOT\ACPI_HAL\0000                         : acpiapic_mp
Modified 1 hardware ID(s).
```

次のコマンドを使用して、 [ **DevCon 更新**](devcon-update.md) HAL のドライバーを更新する操作。

```
devcon update c:\windows\inf\hal.inf acpiapic_mp
```

次に、DevCon には、次の成功メッセージが表示されます。

```
Updating drivers for acpiapic_mp from c:\windows\inf\hal.inf.
Drivers updated successfully.
```

 

 






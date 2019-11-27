---
title: ブロックを登録するための IRP_MN_REGINFO と IRP_MN_REGINFO_EX の処理
description: ブロックを登録するための IRP_MN_REGINFO と IRP_MN_REGINFO_EX の処理
ms.assetid: 2c17fc63-3c33-4d03-8c46-8d56242556d1
keywords:
- WMI WDK カーネル、WMI への登録
- WMI データプロバイダーの登録
- データプロバイダー WDK WMI
- ドライバー登録 WDK WMI
- イベントブロック WDK WMI
- WDK WMI をブロックする
- IRP_MN_REGINFO
- IRP_MN_REGINFO_EX
- 登録 (ブロックを)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 485ce2085cc8c4d5f69dc99ef6ae1ec98d9c4d35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836494"
---
# <a name="handling-irp_mn_reginfo-and-irp_mn_reginfo_ex-to-register-blocks"></a>IRP\_を処理する\_REGINFO と IRP\_\_\_を処理し、レジスタブロックに登録します。





Windows 98 および Windows 2000 では、システムは[**IRP\_の\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)要求をドライバーに送信して、ドライバーがその WMI クラスを登録できるようにします。 Windows XP 以降では、システムによって、 [**IRP\_\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)要求が代わりに送信されます。 ほとんどのドライバーは、コールバックルーチンを提供するために、このような要求を使用[**して、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)これらの要求を処理できます。 詳細について[は、「WMI ライブラリを使用したブロックの登録」を](using-the-wmi-library-to-register-blocks.md)参照してください。

ドライバーでは、動的なインスタンス名を使用するブロックの登録またはドライバー定義の静的インスタンス名の一覧を使用するブロックの登録を要求する **\_reginfo**または**irp\_\_\_** により、irp\_を処理する必要があります。このようなブロックを登録するために、 **Wmi コントロール**を呼び出すことはできません。 ドライバーは必要に応じてこの要求を処理し、PDO またはドライバーで定義された基本名文字列に基づいて静的インスタンス名を使用するブロックを登録できます。

この場合、ドライバーは次のようになります。

1.  [**は、次**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow)のように指定されているパラメーターで、 **wmi. Buffer**に設定されます。

    -   ドライバーによって提供されるすべての登録データのバイト数。これには、他のドライバーの代わりに提供されるデータも含まれます。

    -   ドライバーのレジストリパス。

    -   ドライバーの MOF リソースの名前。

    -   登録するブロックの数。

    -   各ブロックに対して1つずつの、一連の[**Wmi Regguid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)構造体。

2.  各ブロックに対して、ドライバーは次のように指定された**Wmi Regguid**構造体を入力します。

    -   ブロックを表す GUID。

    -   ブロックが収集に負荷がかかるかどうかなど、インスタンス名およびブロックのその他の特性に関する情報を提供するフラグ。 詳細については、「 [WMI 登録フラグ](wmi-registration-flags.md)」を参照してください。

    ブロックが静的インスタンス名で登録されている場合、ドライバーは次のいずれかのメンバーを設定して、ブロックの静的インスタンス名データを指定します。

    -   ドライバーに\_よって、InstanceNameList フラグ\_インスタンス\_一覧に**フラグ**が設定されている場合は、が静的インスタンス名の文字列のリストへのオフセットに設定されます。 WMI は、このリストにインデックスを指定して後続の要求のインスタンスを指定します。

    -   ドライバーによって、BaseNameOffset フラグが\_インスタンス\_インスタンス\_に**フラグ**が設定されている場合は、がベース名文字列へのオフセットに設定されます。 WMI はこの文字列を使用して、ブロックの静的インスタンス名を生成します。

    -   ドライバーによっ\_て、AddDevice フラグ\_インスタンス\_PDO に**フラグ**が設定されている場合は、ドライバーの[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンに渡される pdo に**pdo**が設定されます。 WMI は PDO のデバイスインスタンスパスを使用して、ブロックの静的インスタンス名を生成します。 **IRP\_\_REGINFO\_EX**要求を処理する場合、ドライバーは**Pdo**で渡された物理デバイスオブジェクトで[**obreferenceobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)ルーチンを呼び出す必要があります。 (オブジェクトを逆参照するために、システムは自動的に[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を呼び出します。ドライバーはこの操作を行わないでください)。

    ドライバーは、 **InstanceNameList** **またはベース名**で示されるオフセットに、インスタンス名文字列またはベース名文字列を書き込みます。

3.  ドライバーが別のドライバーの代わりにブロックを登録している場合 (miniclass ドライバーの代わりにクラスドライバーとして)、ドライバーは、別の[**Wmi Reginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow)構造体と、の登録情報を含む一覧表示[**regguid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)構造体のリストを入力します。その他のドライバーのブロックでは、最初の**wmi Reginfo**の**Nextwmireginfo**が **、最初の**設定元から2番目の**wmi reginfo**構造体の先頭までのオフセット (バイト単位) に設定されます。

 

 





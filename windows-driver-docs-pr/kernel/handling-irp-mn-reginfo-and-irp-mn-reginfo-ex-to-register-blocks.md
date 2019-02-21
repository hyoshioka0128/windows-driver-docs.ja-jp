---
title: ブロックを登録するには、IRP_MN_REGINFO および IRP_MN_REGINFO_EX の処理
description: ブロックを登録するには、IRP_MN_REGINFO および IRP_MN_REGINFO_EX の処理
ms.assetid: 2c17fc63-3c33-4d03-8c46-8d56242556d1
keywords:
- WMI の WDK カーネルでは、WMI に登録します。
- WMI データ プロバイダーを登録します。
- WDK の WMI のデータ プロバイダー
- ドライバー WDK WMI の登録
- イベントは、WDK の WMI をブロックします。
- WDK の WMI をブロックします。
- IRP_MN_REGINFO
- IRP_MN_REGINFO_EX
- ブロックを登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60860c450401e03b7f38c53bde34a3fa836b7c72
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537183"
---
# <a name="handling-irpmnreginfo-and-irpmnreginfoex-to-register-blocks"></a>IRP の処理\_MN\_REGINFO と IRP\_MN\_REGINFO\_ブロックを登録する例。





システムは Windows 98 および Windows 2000 で、送信、 [ **IRP\_MN\_REGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551731)をその WMI クラスを登録するためのドライバーを許可するドライバーに要求します。 Windows xp 以降、システムは、送信、 [ **IRP\_MN\_REGINFO\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff551734)代わりに要求します。 ほとんどのドライバーを使用してこれらの要求を処理できる[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)コールバック ルーチンを提供します。 参照してください[ブロックの登録に WMI ライブラリを使用して](using-the-wmi-library-to-register-blocks.md)詳細についてはします。

ドライバーを処理する必要があります**IRP\_MN\_REGINFO**または**IRP\_MN\_REGINFO\_EX**動的ブロックを登録する要求インスタンス名またはドライバーの定義済みの静的インスタンス名のリストを使用します。呼び出すことができない**WmiSystemControl**このようなブロックを登録します。 ドライバーは、PDO またはドライバーの定義の基本名文字列に基づいて静的インスタンス名を使用するブロックを登録するには、この要求を必要に応じて処理できます。

この場合は、ドライバー。

1.  入力、 [ **WMIREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565832)で構造体**Parameters.WMI.Buffer**を指定します。

    -   別のドライバーの代わりに渡されるデータを含む、ドライバーによって提供されるすべての登録データのバイト数。

    -   ドライバーのレジストリのパス。

    -   ドライバーの MOF リソースの名前。

    -   登録するブロックの数。

    -   配列の[ **WMIREGGUID** ](https://msdn.microsoft.com/library/windows/hardware/ff565827)ブロックごとに 1 つの構造します。

2.  各ブロックに対して、ドライバーの設定、 **WMIREGGUID**構造体を指定します。

    -   ブロックを表す GUID。

    -   ブロックが収集する高コストかどうかなど、インスタンス名と、ブロックの他の特性に関する情報を提供するフラグ。 詳細については、次を参照してください。 [WMI 登録フラグ](wmi-registration-flags.md)します。

    静的なインスタンスの名前を持つ、ブロックが登録されている場合、静的なインスタンス名のデータ ブロックを指定する次のメンバーのいずれかのドライバーを設定します。

    -   ドライバーが設定されている場合**フラグ**WMIREG で\_フラグ\_インスタンス\_設定一覧で、 **InstanceNameList**静的インスタンス名の文字列のリストへのオフセットにします。 WMI は、このリストにインデックスを使用して後続の要求でのインスタンスを指定します。

    -   ドライバーが設定されている場合**フラグ**WMIREG で\_フラグ\_インスタンス\_設定 BASENAME、 **BaseNameOffset**基本名文字列へのオフセットにします。 WMI では、この文字列を使用して、ブロックの静的インスタンス名を生成します。

    -   ドライバーが設定されている場合**フラグ**WMIREG で\_フラグ\_インスタンス\_設定 PDO、 **Pdo** PDO ドライバーに渡される[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。 WMI では、ブロックの静的インスタンス名を生成するのに、PDO のデバイスのインスタンスのパスを使用します。 処理するときに、 **IRP\_MN\_REGINFO\_EX**要求と、ドライバーを呼び出す必要があります、 [ **ObReferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff558678)で日常的な物理デバイス オブジェクトが渡された**Pdo**します。 (システムは自動的に呼び出す[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)オブジェクトを逆参照する、ドライバーで実行する必要があります)。

    ドライバーは、インスタンス名の文字列またはで示されたオフセットの基本名文字列を書き込みます**InstanceNameList**または**BaseName**、それぞれします。

3.  場合 (クラス ドライバーは、miniclass ドライバーに代わって可能性があります) として、ドライバーは別のドライバーの代わりのブロックを登録は、別のドライバーが[ **WMIREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565832)構造体のリストと[**WMIREGGUID** ](https://msdn.microsoft.com/library/windows/hardware/ff565827)構造体に、その他のドライバーのブロックの登録情報を使用し、設定**NextWmiRegInfo**最初**WMIREGINFO**最初の先頭からバイトのオフセットに**WMIREGINFO** 、2 つ目の先頭に**WMIREGINFO**構造体。

 

 





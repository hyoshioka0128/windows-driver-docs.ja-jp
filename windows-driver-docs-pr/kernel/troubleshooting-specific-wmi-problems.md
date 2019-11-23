---
title: WMI に関する特定の問題のトラブルシューティング
description: WMI に関する特定の問題のトラブルシューティング
ms.assetid: 966191e7-aec4-4eff-b975-99a6d3eb8d02
keywords:
- WMI WDK カーネル、トラブルシューティング
- WMI の問題のトラブルシューティング WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cef8bff1b2760391403a40c5999735fd8f79d74
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836111"
---
# <a name="troubleshooting-specific-wmi-problems"></a>WMI に関する特定の問題のトラブルシューティング





### <a href="" id="driver-s-wmi-classes-do-not-appear-in-the--root-wmi-namespace"></a>ドライバーの WMI クラスが \\のルート\\wmi 名前空間に表示されない

1.  [Wmimofck](using-wmimofck-exe.md)を使用して、バイナリ MOF ファイル形式が正しいかどうかを確認します。 Mofcomp.exe に追加のエラーメッセージが表示される場合があります。

2.  [システムイベントログ](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-irps-and-the-system-event-log-kg)を調べて、登録要求に応答して、ドライバーが間違った形式の[**wmi reginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow)データ構造を返しているかどうかを確認します。

3.  ドライバーが、 **RegistryPath**と**MofResourceName**の正しい値を、 **[wmi reginfo]** 構造体内で返していることを確認します。

4.  ドライバーが別のファイルに MOF データを提供する場合は、ドライバーの[MofImagePath](setting-the-mofimagepath-registry-value.md)レジストリ値が正しく設定されていることを確認します。

5.  [WMI WDM プロバイダーログ](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-wdm-provider-log-kg)でエラーを確認します。

6.  [Mofcomp.exe](compiling-a-driver-s-mof-file.md)を使用して、MOF テキストファイルの再コンパイルと再読み込みを行います。 たとえば、コマンド**mofcomp.exe: root/wmi ドライバー** .mof は、ドライバー .mof ファイル内のすべての mof データの再コンパイルと再読み込みを試みます。 Mofcomp.exe が mofcomp.exe に生成するエラーメッセージを確認します。 ( **\#定義**などのプリプロセッサディレクティブを mof ファイルで使用する場合は、元のソースファイルではなく、既に前処理された MOF ファイルを使用する必要があることに注意してください。

    **警告**  この操作が成功すると、新しい WMI クラスデータがシステムに実際に登録されます。 ドライバーの MOF データが正しく読み取られているかどうかをテストするには、(たとえば、Wbemtest を使用して) これらのクラスを削除する必要があります。

     

7.  前の手順が成功した場合、最も可能性の高い問題は、 **MofResourceName**などの、指定された**情報**のメンバーが正しく指定されていないことです。 または、MOF ファイルで、存在しない基底クラスから派生したクラスが指定されている可能性があります。

8.  ドライバーが動的な MOF データ (「[動的 Mof データの実装](implementing-dynamic-mof-data.md)」を参照) を使用している場合は、ドライバーが MSWmi\_MOFDATA\_GUID guid に対する WMI IRP 要求を受信していることと、IRP が正常に完了し、エラーがログに記録されていないことを確認します。

### <a name="drivers-wmi-properties-or-methods-cannot-be-accessed"></a>ドライバーの WMI のプロパティまたはメソッドにアクセスできません

1. Wmimofck を使用して、バイナリ MOF ファイル形式が正しいかどうかを確認し**ます。** 詳細については、「 [Using wmimofck](using-wmimofck-exe.md)」を参照してください。

2. システムイベントログでエラーを確認します。 詳細については、「 [WMI irp とシステムイベントログ](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-irps-and-the-system-event-log-kg)」を参照してください。

3. [WMI WDM プロバイダーログ](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-wdm-provider-log-kg)でエラーを確認します。

4. Wbemtest を使用してドライバーのクラスにクエリを実行するたびに、ドライバーが WMI IRP を受信するようにしてください。 それ以外の場合は、MOF ファイル内の指定された GUID が、ドライバーが想定している GUID と一致していることを確認します。 また、ドライバーが WMI 登録要求を受信していること、成功していること、およびドライバーが適切な Guid を登録していることを確認します。

5. ドライバーが IRP を受信する場合は、IRP が正常に完了していること、およびドライバーが適切な種類の**Wnode\_* XXX*** 構造を返していることを確認します。

6. Wbemtest でエラーが返された場合は、 **[詳細情報]** ボタンをクリックし、**説明**のプロパティでエラーの説明を確認します。

7. メソッドについては、ドライバーが[**irp\_の\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)をサポートしていることを確認します。これは、すべての\_データを\_、irp\_、メソッドの GUID に対する[**単一の\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)要求を\_します。\_ WMI は、メソッドを実行する前に、これら2つの要求のいずれかを常に実行します。

### <a name="drivers-wmi-events-are-not-being-received"></a>ドライバーの WMI イベントが受信されていません

1.  [システムイベントログ](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-irps-and-the-system-event-log-kg)でエラーを確認します。 たとえば、 [**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)を呼び出すときにドライバーが静的イベント名を指定しても、ドライバーが静的イベント名を登録しなかった場合、システムイベントログにエントリが生成されます。

2.  [WMI WDM プロバイダーログ](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-wdm-provider-log-kg)でエラーを確認します。

3.  ドライバーがイベント参照を送信する場合、ドライバーは、イベント参照を送信した直後に、[**単一\_インスタンスの要求\_、IRP\_の\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)を受信する必要があります。 ドライバーが IRP を受信しない場合、 [**Wnode\_イベント\_参照**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_reference)構造の形式が正しくない可能性があります。 ドライバーが IRP を受信した場合、状態が [成功]\_正常に完了している必要があります。

4.  ドライバーが[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)を使用してイベントまたはイベント参照を送信する場合は、イベント構造 ( [**WNODE\_SINGLE\_INSTANCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)または**WNODE\_event\_reference**) が正しく入力されていることを確認します。 特に、イベント GUID が静的インスタンス名に登録されている場合は、正しいインスタンスインデックスとプロバイダー ID が指定されていることを確認してください。 イベント GUID が動的インスタンス名に登録されている場合は、イベントが送信されるときにインスタンス名が含まれていることを確認してください。 **Wnode\_イベント\_参照**構造を使用してイベントを指定する場合は、 **Wnode**が**targetguid**と一致することを確認します。

5.  ドライバーが[**WmiFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent)を使用してイベントを送信する場合は、 *Guid*および*instanceindex*パラメーターに正しい値が渡されていることを確認してください。

### <a name="changes-in-security-settings-for-wmi-requests-do-not-take-effect"></a>WMI 要求のセキュリティ設定の変更が有効にならない

-   WMI WDM プロバイダーをアンロードして再読み込みします。 "WMI REG\_フラグ\_高コストのフラグ" で登録された WMI データブロックの場合、プロバイダーは、そのブロックのコンシューマーが存在する限り、データブロックのハンドルを開いたままにします。 プロバイダーがハンドルを閉じるまで、新しいセキュリティ設定は有効になりません。 プロバイダーのアンロードと再読み込みを行うと、ハンドルが閉じられていることを確認します。 (WMI REG\_フラグ\_高額なフラグの詳細については、「 [**Wmi Regguid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)」を参照してください)。

 

 





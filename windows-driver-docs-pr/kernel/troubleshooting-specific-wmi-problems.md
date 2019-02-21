---
title: 特定の WMI のトラブルシューティング
description: 特定の WMI のトラブルシューティング
ms.assetid: 966191e7-aec4-4eff-b975-99a6d3eb8d02
keywords:
- WMI の WDK のカーネルのトラブルシューティング
- WDK の WMI に関する問題のトラブルシューティング
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1759ae885a46d2e8a45e08e5916ac25ca7723025
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529441"
---
# <a name="troubleshooting-specific-wmi-problems"></a>特定の WMI のトラブルシューティング





### <a href="" id="driver-s-wmi-classes-do-not-appear-in-the--root-wmi-namespace"></a>ドライバーの WMI クラスには表示されません、\\ルート\\wmi Namespace

1.  使用[wmimofck](using-wmimofck-exe.md)driver.bmf バイナリの MOF ファイルの形式が正しいかどうかを確認します。 Mofcomp.log に関連するエラー メッセージがあります。

2.  チェック、[システム イベント ログ](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-irps-and-the-system-event-log-kg)かどうか、ドライバーは、不適切な返すことを確認する[ **WMIREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565832)登録要求への応答内のデータ構造。

3.  ドライバーに適切な値を返すことを確認**RegistryPath**と**MofResourceName**内、 **WMIREGINFO**構造体。

4.  ドライバーは、別のファイルには、その MOF データを提供する場合はことを確認、 [MofImagePath](setting-the-mofimagepath-registry-value.md)ドライバーのレジストリ値が正しく設定されています。

5.  チェック、 [WMI WDM プロバイダー ログ](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-wdm-provider-log-kg)エラー。

6.  使用[Mofcomp](compiling-a-driver-s-mof-file.md)を再コンパイルして MOF テキスト ファイルを再読み込みします。 たとえば、次のコマンド**mofcomp N: 気**は再コンパイルして driver.mof ファイル内のすべての MOF データを再読み込みを試みます。 Mofcomp.log Mofcomp、どのようなエラー メッセージを表示するチェックが生成されます。 (なお、MOF ファイルのプリプロセッサ ディレクティブはなどで使用する場合**\#定義**、既に前処理された MOF ファイルと元のソース ファイルではなくを使用する必要があります。

    **警告**  システムを新しい WMI クラスのデータに実際には登録が成功すると、この操作。 これらのクラスを (たとえば、Wbemtest を使用して) を削除する必要があります、ドライバーの MOF データが正しく読み取られている場合をテストします。

     

7.  前の手順が成功したかどうかは、最も可能性の高い問題なのメンバーは**WMIREGINFO**など**MofResourceName**、正しく指定されていません。 また、問題でした、MOF ファイルが存在しない基本クラスから派生したクラスを指定することがあります。

8.  ドライバーは、動的な MOF データを使用している場合 (を参照してください[動的 MOF データを実装する](implementing-dynamic-mof-data.md))、ドライバーが、MSWmi の IRP の WMI 要求を受信しているかを確認\_MofData\_GUID GUID と IRP が終了します。正常にして、エラーは記録されます。

### <a name="drivers-wmi-properties-or-methods-cannot-be-accessed"></a>ドライバーの WMI のプロパティまたはメソッドにアクセスすることはできません。

1. 使用**wmimofck driver.bmf**バイナリの MOF ファイルの形式が正しいかどうかを確認します。 詳細については、次を参照してください。 [wmimofck.exe を使用して](using-wmimofck-exe.md)します。

2. システム イベント ログのエラーを確認します。 詳細については、次を参照してください。[とシステム イベント ログの WMI Irp](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-irps-and-the-system-event-log-kg)します。

3. チェック、 [WMI WDM プロバイダー ログ](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-wdm-provider-log-kg)エラー。

4. Wbemtest を使用して、ドライバーのクラスのクエリを実行するたびに、ドライバーが WMI IRP を受信することを確認します。 それ以外の場合は、チェックの MOF ファイルで指定された GUID が、ドライバーの GUID と一致することを指定してください。 また、ドライバーが、それが成功すると、WMI 登録要求を受信し、ドライバーが適切な Guid を登録することを確認します。

5. ドライバーは IRP を受信する場合は、IRP が正常に完了したことと、適切な種類のドライバーに返すことを確認します**れた WNODE\_* XXX*** 構造体。

6. Wbemtest がエラーを返した場合にクリックして、**詳細**ボタンをクリックし、確認、**説明**エラーの説明のプロパティ。

7. 方法については、確認には、ドライバーが処理をサポートしている、 [ **IRP\_MN\_クエリ\_すべて\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff551650)と[ **IRP\_MN\_クエリ\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff551718)メソッドの GUID を要求します。 WMI はメソッドを実行する前に、2 つの要求の 1 つを実行して常にします。

### <a name="drivers-wmi-events-are-not-being-received"></a>ドライバーの WMI イベントが受信されていません

1.  チェック、[システム イベント ログ](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-irps-and-the-system-event-log-kg)エラー。 たとえばを呼び出すときに、ドライバーは、静的イベント名を指定します[ **IoWMIWriteEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff550520)がドライバーでは、静的イベント名が登録されませんでした、これが、システム イベント ログ内のエントリを生成します。

2.  チェック、 [WMI WDM プロバイダー ログ](general-techniques-for-testing-wmi-driver-support.md#ddk-wmi-wdm-provider-log-kg)エラー。

3.  ドライバーが、イベントの参照を送信する場合、ドライバーが受信する必要があります、 [ **IRP\_MN\_クエリ\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff551718)すぐに要求イベントの参照を送信します。 ドライバーは IRP を受信しなかった場合、 [**れた WNODE\_イベント\_参照**](https://msdn.microsoft.com/library/windows/hardware/ff566374)構造が正しくないれた可能性があります。 ドライバーは IRP を受信する場合にする必要がある完了の状態で\_成功します。

4.  ドライバーで使用する場合[ **IoWMIWriteEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff550520)イベントまたはイベントの参照を送信することを確認しますイベント構造 (か[**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)または**れた WNODE\_イベント\_参照**)、正しく入力します。 具体的には、イベントの GUID が静的なインスタンス名には登録されていることを確認して、適切なインスタンスのインデックスとプロバイダーの ID が提供されます。 イベントの動的インスタンス名に GUID が登録されていることを確認する場合、イベントが送信されるときにインスタンス名が含まれるです。 使用する場合、**れた WNODE\_イベント\_参照**イベントを指定することを確認の構造体**Wnode.Guid**と一致する**TargetGuid**します。

5.  ドライバーで使用する場合[ **WmiFireEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff565807)イベントを送信することを確認、適切な値が渡されました、 *Guid*と*InstanceIndex*パラメーター。

### <a name="changes-in-security-settings-for-wmi-requests-do-not-take-effect"></a>WMI の要求のセキュリティ設定の変更は反映されません。

-   アンロードし、WMI プロバイダーを再読み込みします。 WMI データ ブロックが登録されている、WMIREG の\_フラグ\_高価なフラグは、プロバイダー ハンドルを開いたままデータ ブロックにそのブロックのコンシューマーがある限り、します。 プロバイダーは、ハンドルを終了するまで、新しいセキュリティ設定は有効になりません。 アンロードして、プロバイダーを再読み込みにより、ハンドルが閉じられました。 (詳細については、WMIREG\_フラグ\_高価なフラグを参照してください[ **WMIREGGUID**](https://msdn.microsoft.com/library/windows/hardware/ff565827))。

 

 





---
title: オーディオのプロパティのハンドラー
description: オーディオのプロパティのハンドラー
ms.assetid: 4bf176ae-b3fd-47e6-9802-a92ef5e9904f
keywords:
- WDK、ハンドラーのオーディオのプロパティ
- WDM オーディオ プロパティ WDK、ハンドラー
- ハンドラーの WDK オーディオ
- プロパティ ハンドラー WDK オーディオ
- WDK オーディオのプロパティの設定
- プロパティの get WDK オーディオ
- basic - クエリ WDK オーディオをサポート
- automation テーブル WDK オーディオ
- プロパティ ハンドラーのオーディオ、WDK をフィルター処理します。
- プロパティ ハンドラーのオーディオ、WDK をピン留め
- ノード WDK オーディオ、プロパティ ハンドラー
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3c33f8bd792e46e14e98061e59a236e13c625805
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560898"
---
# <a name="audio-property-handlers"></a>オーディオのプロパティのハンドラー


## <span id="audio_property_handlers"></span><span id="AUDIO_PROPERTY_HANDLERS"></span>


ミニポート ドライバーでサポートされている各プロパティに関する情報を格納する、 [ **PCPROPERTY\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff537722)構造体。 この構造体には、プロパティの詳細については、次の情報が含まれています。

-   プロパティ セット GUID およびプロパティ ID (またはインデックス)

-   プロパティのハンドラー ルーチンへの関数ポインター

-   ハンドラーをサポートするプロパティの操作を指定するフラグ

ミニポート ドライバーは、automation のテーブルを提供します (で指定された、 [ **PCAUTOMATION\_テーブル**](https://msdn.microsoft.com/library/windows/hardware/ff537685)構造) フィルター。 ノードの種類が独自のテーブルまたはドライバーが、フィルターの暗証番号 (pin) の型とノード型の各ピン テーブルの追加のオートメーションを提供します。 Automation の各テーブルには、PCPROPERTY の (場合によっては空) の配列が含まれています。\_項目の構造体、および各構造体は、フィルター、pin、またはノードの 1 つのプロパティについて説明します。 クライアントは、フィルター、pin、またはノードをプロパティ要求を送信するポート ドライバーは、automation テーブルを介して要求を適切なプロパティのハンドラーにルーティングされます。

ミニポート ドライバーでは、各プロパティの一意のプロパティ ハンドラー ルーチンを指定できます。 ただし、ドライバーは、いくつかのようなプロパティを処理する場合これらできる場合があります統合便宜上 1 つのハンドラー ルーチンです。 ドライバー開発者が作成した実装上の決定は、各プロパティの一意のハンドラーを指定するか、単一のハンドラーにいくつかのプロパティを統合するプロパティの要求を送信するクライアントに対して透過的である必要があります。

ユーザー モードのクライアントは Microsoft Win32 関数を呼び出すことによって取得、セット、またはプロパティの基本サポート要求を送信できます[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)で、 *dwIoControlCode*を呼び出すパラメーターには、IOCTL 設定\_KS\_プロパティ。 オペレーティング システムがこの呼び出しに変換する[ **IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)、クラス ドライバーにディスパッチします。 詳細については、[KS プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff567671)を参照してください。

クライアントが KS プロパティの要求を送信します (IOCTL では、\_KS\_プロパティ I/O-コントロール IRP) フィルター ハンドルまたは暗証番号 (pin) のハンドルでは、KS システム ドライバー (Ks.sys) は、フィルター オブジェクトまたは pin オブジェクト用のポート ドライバーへの要求を提供します。 ミニポート ドライバーでは、プロパティのハンドラーを提供する場合、ポート、ドライバーは、ハンドラーに要求を転送します。 要求を転送する前に、ポート ドライバー情報を変換しますプロパティ要求で指定された形式に、 [ **PCPROPERTY\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff537723)構造体。 ポートのドライバーでは、この構造体をミニポート ドライバーのハンドラーに渡します。

**MajorTarget** PCPROPERTY のメンバー\_オーディオ デバイスのプライマリのミニポート ドライバー インターフェイスを指す要求。 たとえば、WavePci デバイスは、これは、ミニポート ドライバー オブジェクトへのポインター [IMiniportWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536724)インターフェイス。

フィルターのハンドルに送信される KS プロパティ要求の場合、 **MinorTarget** PCPROPERTY のメンバー\_要求が**NULL**します。 暗証番号 (pin) のハンドルに送信される要求の場合**MinorTarget**暗証番号 (pin) のストリーム インターフェイスを指します。 ストリーム オブジェクトへのポインターは、この WavePci デバイスは、たとえば、 [IMiniportWavePciStream](https://msdn.microsoft.com/library/windows/hardware/ff536725)インターフェイス。

**インスタンス**と**値**PCPROPERTY のメンバー\_KS プロパティ要求のそれぞれを要求がポイントして、入力と出力バッファー。 (バッファーがで指定された、 *lpInBuffer*と*lpOutBuffer*のパラメーター、 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)関数です)。これらのバッファーには、それぞれで説明するプロパティ記述子 (インスタンス データ) とプロパティの値 (操作データ) が格納[オーディオ ドライバーのプロパティ セット](https://msdn.microsoft.com/library/windows/hardware/ff536197)します。 **値**、出力バッファーの先頭を指すメンバーが、**インスタンス**ポインター入力バッファーの先頭からのオフセットです。

入力バッファーがいずれかで始まる、 [ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)または[ **KSNODEPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff537143)構造体。 ポートのドライバーでは、この構造体の情報をコピー、PCPROPERTY に\_要求構造体の**ノード**、 **PropertyItem**、および**動詞**メンバー。 ポートのドライバーが読み込まれるすべてのデータは、バッファーに KSPROPERTY または KSNODEPROPERTY 構造に従っての場合、**インスタンス**このデータへのポインターを持つメンバー。 それ以外の場合、設定**インスタンス**に**NULL**します。

ポート ドライバーが、PCPROPERTY を設定して、入力バッファーがノードの情報を含まない、KSPROPERTY 構造体で始まる場合\_要求構造体の**ノード**ULONG(-1) するメンバー。 ここで、ポート ドライバーは、フィルターまたはフィルターのハンドルまたは暗証番号 (pin) のハンドルによってプロパティ要求のターゲットを指定するかどうかに応じて、pin、ミニポート ドライバーのオートメーションのテーブルから適切なハンドラーを呼び出します。 (テーブルでは、プロパティのハンドラーを指定しない場合、ポート ドライバー要求を処理、代わりにします。)

場合、入力バッファーの先頭 KSNODEPROPERTY 構造体が、ポート ドライバー ノード ID この構造体からにコピー、PCPROPERTY\_要求構造体の**ノード**メンバーから適切なハンドラーを呼び出すと、ノードのミニポート ドライバーのオートメーション テーブルです。 (ここでも、テーブルでは、プロパティのハンドラーを指定しない場合、ポート ドライバー要求を処理代わりにします。)

ポート ドライバー チェック、KSPROPERTY\_型\_KSPROPERTY または KSNODEPROPERTY、2 つの構造を決定するプロパティの要求の操作フラグのビット トポロジは、入力バッファーの先頭が存在します。

-   このビットが設定されている場合はノードのプロパティを要求し、入力バッファーが KSNODEPROPERTY 構造で始まります。

-   それ以外の場合、入力バッファーから始まります KSPROPERTY 構造体。

KSPROPERTY の詳細については\_型\_トポロジを参照してください[ **KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)します。

PCPROPERTY\_要求構造体の**InstanceSize**と**ValueSize**メンバーが指すバッファーのサイズを指定する、**インスタンス**と**値**メンバー。 **ValueSize**プロパティの要求の出力バッファーのサイズと同じですが、 **InstanceSize**は入力バッファーに KSPROPERTY または KSNODEPROPERTY 構造に従っているデータのサイズです。 つまり、 **InstanceSize** KSPROPERTY または KSNODEPROPERTY 構造体のサイズ-入力バッファーのサイズです。 この構造体を適合する追加のデータ ポート ドライバー設定**InstanceSize**をゼロに (と**インスタンス**に**NULL**)。

たとえば、クライアントが指定されている場合、 [ **KSNODEPROPERTY\_オーディオ\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff537145)ポート ドライバー、入力バッファー内のインスタンス データと構造体は、ハンドラーに渡します、PCPROPERTY\_要求が構造体が**インスタンス**メンバーが、KSNODEPROPERTY を指す\_オーディオ\_チャネル構造体の**チャネル**メンバー、およびその**InstanceSize**メンバーには、値が含まれています。

**sizeof**(KSNODEPROPERTY\_オーディオ\_チャネル)- **sizeof**(KSNODEPROPERTY)

プロパティ値を取得するプロパティの get 要求を送信する前に、クライアントは、ミニポート ドライバーのプロパティのハンドラーがプロパティの値を書き込むことができます、出力バッファーを割り当てる必要があります。 一部のプロパティの出力バッファーのサイズは、デバイスに依存する、およびクライアントが必要なバッファー サイズのプロパティのハンドラーをクエリする必要があります。 このような場合は、クライアントは、nullptr の出力バッファー ポインターと、出力バッファーの長さが 0 で、プロパティの初期要求を送信します。 ハンドラーは、状態コード STATUS_BUFFER_OVERFLOW と共に必要なバッファー サイズを返すことで応答します。 次に、クライアントは 2 番目のプロパティの get 要求でこのバッファーを送信する指定されたサイズの出力バッファーを割り当てることで、プロパティ値を取得します。
 
指定されたバッファー サイズが小さすぎて要求された情報が表示される場合、メソッドは STATUS_BUFFER_TOO_SMALL を返します。 
 
場合によっては、PortCls ポートのドライバーは、0 以外の出力バッファーのアドレスのサイズとプロパティの要求に応答 STATUS_BUFFER_TOO_SMALL STATUS_BUFFER_OVERFLOW ではなくを返します。 必要なバッファー サイズは、このような場合は返されません。 
 
詳細については、次を参照してください。 [NTSTATUS 値を使用して](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)と次のブログ投稿。

- [その後の操作に必要なバイト数を返す方法](https://blogs.msdn.microsoft.com/doronh/2006/12/12/how-to-return-the-number-of-bytes-required-for-a-subsequent-operation/)

- [STATUS_BUFFER_OVERFLOW 本当に名前を付ける STATUS_BUFFER_OVERFLOW_PREVENTED](https://blogs.msdn.microsoft.com/oldnewthing/20080404-00/?p=22863)




 

 





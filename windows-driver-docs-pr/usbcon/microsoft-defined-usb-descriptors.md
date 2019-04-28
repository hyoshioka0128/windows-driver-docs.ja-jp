---
Description: Microsoft では、一連の独自のデバイス クラスと Microsoft OS ディスクリプター (カスタム設定) と呼ばれる USB 記述子を提供します。
title: USB デバイス向けの Microsoft OS 記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d08d4c9850338fc9e23ca57c2f61d3864fd513e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379932"
---
# <a name="microsoft-os-descriptors-for-usb-devices"></a>USB デバイス向けの Microsoft OS 記述子


**要約**

-   [Microsoft OS 1.0 記述子の仕様](https://go.microsoft.com/fwlink/p/?linkid=617154)
-   [Microsoft OS 2.0 記述子の仕様](https://go.microsoft.com/fwlink/p/?linkid=306681)

Microsoft では、一連の独自のデバイス クラスと Microsoft OS ディスクリプター (カスタム設定) と呼ばれる USB 記述子を提供します。




複数のハードウェア機能が含まれているデバイスの高速の登場により多くの製造元は、自分のデバイスが、現在のユニバーサル シリアル バス (USB) デバイス クラスのいずれかに問題なく適合しないことを紹介します。 このような製造元の USB テクノロジの最も魅力的な機能の 1 つを deprives これは、: (デバイスのクラス) に従ってドライバー ソフトウェアの標準化します。 Microsoft Windows では、ほとんどの標準の USB デバイス クラスに属しているデバイスのネイティブ クラス ドライバーが用意されていて、これらのドライバーには、エンドユーザーがこのようなデバイスをコンピューターに特別なソフトウェアをインストールすることがなく簡単に接続ができるようにします。

製造元がデバイスの USB デバイス クラスの現在のセットにも適合しないを対応するために Microsoft Corporation は、一連の独自のデバイス クラスと Microsoft OS ディスクリプター (カスタム設定) と呼ばれる USB ディスクリプターを開発しました。 アプリケーションとシステム ソフトウェアの両方では、カスタム設定をサポートするかどうかを判断するデバイスを照会することによって、Microsoft によって定義されたクラスに属するデバイスを識別できます。

Microsoft OS ディスクリプターには、独自のデバイス クラスをサポートしている以外の重要な用途があります。 具体的には、デバイスのファームウェアから最大のメリットを派生させるためのメカニズムを提供します。 Microsoft OS ディスクリプターを利用して、ヘルプ ファイル、特別なアイコン、Uniform Resource Locator (Url)、レジストリ設定、およびインストールが容易になり、顧客満足度を強化するのにために必要なその他のデータを配信するのにファームウェアを使用できます。 場合によっては、配信とアップグレードのサポートを合理化する、フロッピー ディスクや Cd--などの記憶メディアを省略できます。

## <a name="operating-system-support"></a>オペレーティング システムのサポート


Microsoft OS 1.0 記述子でサポートされます。

-   Windows 8.1
-   Windows 8
-   Windows 7
-   Windows Vista、Windows Server 2008
-   Windows XP Service Pack 1 (SP1)、Windows Server 2003

Microsoft OS 2.0 記述子でサポートされます。

-   Windows 8.1

## <a name="why-does-windows-issue-a-string-descriptor-request-to-index-0xee"></a>理由は Windows 文字列記述子に要求を発行インデックス 0 xee でしょうか。


Microsoft OS ディスクリプターをサポートするデバイスは、0 xee の固定文字列インデックス位置にあるファームウェアに特別な USB 文字列記述子を格納する必要があります。 この文字列記述子には、Microsoft OS 文字列記述子が呼び出されます。

-   その存在は、デバイスが 1 つまたは複数の OS 機能の記述子が含まれていることを示します。
-   関連付けられている OS 機能記述子を取得するために必要なデータが含まれています。
-   Ihv は、0 xee に格納することもできますが、その他の文字列から OS の文字列記述子を区別する署名フィールドが含まれています。
-   Microsoft OS ディスクリプターの将来のリビジョンのバージョン番号が含まれています。

0 xee に文字列記述子がない、またはインデックス位置に文字列記述子が有効な OS 文字列記述子ではありません、Windows では、デバイスに、記述子には OS 機能が含まれていないこと前提としています。

新しいデバイスが最初にコンピューターに接続されている場合、Microsoft OS ディスクリプターをサポートするオペレーティング システムがインデックス 0 xee 位置にあることを示す文字列記述子を要求します。 Microsoft OS の文字列記述子には、インデックス 0 xee になる可能性があるその他の文字列を区別するために、オペレーティング システムを使用する埋め込みの署名フィールドが含まれています。 インデックス 0 xee 位置にある適切な署名フィールドが含まれる文字列記述子の存在は、デバイスが Microsoft OS ディスクリプターをサポートしているオペレーティング システムを示します。 Microsoft OS の文字列記述子には、オペレーティング システムのバージョン情報も提供します。

インデックス 0 xee 列挙中にデバイス - デバイスのドライバーが読み込まれる--前に一部のデバイスが正しく機能しない原因と考えられる位置にある文字列記述子のオペレーティング システムのクエリ。 このようなデバイスは Microsoft OS ディスクリプターをサポートする Windows オペレーティング システムのバージョンではサポートされていません。

ユニバーサル シリアル バスの「要求エラー」セクションで説明されている失速パケット (つまり、パケットの停止の種類のパケットの識別子を含む) で応答する必要がありますが、デバイスにインデックス 0 xee 位置にある有効な文字列記述子が含まれていない場合指定。 デバイス、失速パケットに応答しない場合、システムは発行シングル エンド 0 リセット パケットを停止している状態 (Windows XP の場合のみ) から回復するために、デバイスにします。

オペレーティング システムでは、デバイスから Microsoft OS 文字列記述子が要求をした後は、次のレジストリ キーが作成されます。

**HLKM\\SYSTEM\\CurrentControlSet\\Control\\UsbFlags\\*vvvvpppprrrrr***

オペレーティング システムの作成という名前のレジストリ エントリを**osvc**、このデバイスで Microsoft OS ディスクリプターをサポートするかどうかを示すレジストリ キーの下。 デバイスが提供されない場合、最初の有効な応答時間をオペレーティング システムのクエリ Microsoft OS 文字列記述子、オペレーティング システムのことが要求しないようにさらにその記述子。

そのキーの下のレジストリ エントリを参照してください。 [USB デバイスのレジストリ エントリ](usb-device-specific-registry-settings.md)します。

詳細については、次を参照してください。 [Microsoft OS ディスクリプター](https://go.microsoft.com/fwlink/p/?linkid=617154)します。

## <a name="what-types-of-os-feature-descriptors-are-supported-by-windows"></a>Windows では、どのような種類の OS 機能の記述子がサポートされているでしょうか。


機能記述子として格納される情報は、Microsoft が定義されている標準形式のいずれかに準拠する必要があります。 追加の機能の記述子を定義または Microsoft の同意なしで実装できません。 Microsoft には、次の機能の記述子が定義されています。

-   **互換性 ID を拡張**します。 Windows では、クラスとサブクラスのコードを使用して、USB デバイスの適切な既定のドライバーを見つけやすいようにします。 ただし、USB Device Working Group では、これらのコードを割り当てる必要があります。 つまり、多くの場合、新しい種類の機能を実装しているデバイスがまだないクラスとサブクラスの適切なコード、ため、Windows は、コードを使用して既定のドライバーを選択することはできません。 Ihv は、拡張互換性 ID OS 機能記述子とファームウェアの情報を格納することで、この問題を回避できます。 Windows は、デバイスを接続するときに、この情報を取得し、読み込むドライバーを既定値を決定する場合に使用します。
-   **拡張プロパティ**します。 現時点では、プロパティが、USB デバイスを宣言する 2 つのレベルがある: クラス レベルまたは devnode レベル。 OS 機能記述子により、ストアなどのプロパティ - 追加するためにベンダー拡張プロパティは、ページ、Url、およびアイコンでデバイスのファームウェアに役立ちます。

## <a name="related-topics"></a>関連トピック
[Microsoft OS 1.0 記述子の仕様](https://go.microsoft.com/fwlink/p/?linkid=617154)  
[Microsoft OS 2.0 記述子の仕様](https://go.microsoft.com/fwlink/p/?linkid=306681)  
[Windows 用の USB デバイスの構築](building-usb-devices-for-windows.md)  




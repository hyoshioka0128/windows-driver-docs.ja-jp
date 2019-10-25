---
title: アプリケーション ハイブのレジストリ操作のフィルター処理
description: アプリケーションハイブの初期サポートは、Windows Vista で導入されました。
ms.assetid: A8D06E25-7CC6-476A-AB55-DAFE19954347
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f5a2120dc95228d9e677418315bfb173fa082e68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836711"
---
# <a name="filtering-registry-operations-on-application-hives"></a>アプリケーション ハイブのレジストリ操作のフィルター処理


アプリケーションハイブの初期サポートは、Windows Vista で導入されました。 Windows 8 以降では、アプリケーションハイブのサポートが強化されており、アプリケーションハイブの使用量が広くなっています。 このため、これらのバージョンの Windows 用に開発されたレジストリフィルタードライバー (特に Windows 8 以降) では、アプリケーションハイブでのレジストリ操作に注意する必要があります。 これらのドライバーは、ユーザーエクスペリエンスに悪影響を及ぼさないように、このような操作を効率的に処理する必要があります。

アプリケーションハイブは、アプリケーション固有の状態データを格納するためにユーザーモードアプリケーションによって読み込まれるレジストリハイブです。 アプリケーションは、アプリケーションハイブを読み込むために、 [**Regloadappkey**](https://docs.microsoft.com/windows/desktop/api/winreg/nf-winreg-regloadappkeya)関数を呼び出します。

他の種類のレジストリハイブとは異なり、アプリケーションハイブは \\REGISTRY\\MACHINE または \\REGISTRY\\USER の下ではなく、レジストリパス名\\\\レジストリに読み込まれます。 \\レジストリ\\パス名には特別な意味がありますが、このパスを走査する方法はありません。 \\\\レジストリの下でキーを開こうとすると、エラー状態ステータス\_アクセス\_拒否されて失敗します。 アプリケーションがアプリケーションハイブのキーにアクセスする唯一の方法は、アプリケーションハイブのルートキーへのハンドルを使用することです。 アプリケーションは、hive を読み込む**Regloadappkey**呼び出しからこのハンドルを取得します。

アプリケーションでは、アプリケーションハイブを明示的にアンロードする必要はありません。 ハイブへのすべてのハンドルが閉じられると、オペレーティングシステムによってアプリケーションハイブが自動的にアンロードされます。

アプリケーションハイブは、hive 内のキーのセキュリティ記述子の設定をサポートしていません。 代わりに、hive 全体に1つのセキュリティ記述子があります。 アプリケーションハイブのキーにセキュリティ記述子を設定しようとすると、失敗し\_アクセス\_拒否されました。 各キーが独自のセキュリティ記述子で保護されている他の種類のレジストリハイブとは異なり、アプリケーションハイブのセキュリティは hive ファイルのセキュリティ記述子に基づいています。 そのため、hive の読み込みに成功したエンティティは、hive 全体を変更できます。

レジストリフィルタードライバーは、アプリケーションハイブでレジストリ操作を実行するために、その[*Registrycallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)ルーチンへの呼び出しを受信します。 これらの呼び出しでは、アプリケーションハイブのレジストリ操作と他の種類のレジストリハイブに対する操作が区別されません。 作成キーおよびオープンキー操作を処理するレジストリフィルタードライバー ( **Regntpreopenkey**、 **regntpreopenkeyex**、 **RegNtPreCreateKey**、および**regntprecreatekeyex**通知値によって示されます) は、次の特殊な状況を正しく処理します。 アプリケーションハイブが読み込まれると、読み込みプロセスの最後の手順として、レジストリマネージャーによって hive のルートキーが開かれます。 レジストリマネージャーは、キーへの絶対パスを使用してこのオープンキー操作を発行します。これは、Reg\_の**CompleteName**メンバーのパス名の文字列によって[ **\_キー\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_create_key_information)、 [**reg\_create が作成されることを意味 @no__\_情報\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_create_key_information_v1)、 [**REG\_OPEN\_キー\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560957)、または[**REG\_OPEN\_Key\_情報\_v1**](https://msdn.microsoft.com/library/windows/hardware/ff560959)構造は "\\から始まります。レジストリ\\\\"になります。 アプリケーションハイブを開くために絶対パスを使用できるのは、レジストリマネージャーだけです。 レジストリフィルタードライバーがこの方法でアプリケーションハイブを開こうとすると (たとえば、 [**Zwopenkey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)ルーチンを呼び出すことによって)、操作は失敗し、エラー状態状態\_アクセス\_拒否されます。

 

 





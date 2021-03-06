---
title: アプリケーション ハイブのレジストリ操作のフィルター処理
description: アプリケーションのハイブの初期のサポートは、Windows Vista で導入されました。
ms.assetid: A8D06E25-7CC6-476A-AB55-DAFE19954347
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d6b8f8cdd80ba65c881000d3de0e3a5aa5d0f3a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386600"
---
# <a name="filtering-registry-operations-on-application-hives"></a>アプリケーション ハイブのレジストリ操作のフィルター処理


アプリケーションのハイブの初期のサポートは、Windows Vista で導入されました。 Windows 8 以降、アプリケーションのハイブのサポートの向上が使用して、アプリケーション ハイブのより広範囲に利用が必要です。 したがって、フィルター ドライバーのレジストリのバージョンの Windows、および Windows 8 の特に開発し、アプリケーションのハイブをレジストリの操作の認識、後である必要があります。 これらのドライバーでは、ユーザー エクスペリエンスに悪影響を与えるを回避するために効率的には、このような操作を処理する必要があります。

アプリケーションのハイブは、アプリケーション固有の状態データを格納するユーザー モード アプリケーションによって読み込まれたレジストリ ハイブです。 アプリケーションを呼び出す、 [ **RegLoadAppKey** ](https://docs.microsoft.com/windows/desktop/api/winreg/nf-winreg-regloadappkeya)関数をアプリケーションのハイブをロードします。

レジストリ ハイブの他の種類とは対照的アプリケーション ハイブが読み込まれている、\\レジストリ\\レジストリ パス名の代わりに \\レジストリ\\マシンまたは\\レジストリ\\ユーザー。 \\レジストリ\\パス名は、このパスでは、および下キーを開こうとすると移動する方法がないことに特別な\\レジストリ\\A はエラー状態で失敗\_アクセス\_拒否されました。 アプリケーションは、アプリケーションのハイブ内のキーにアクセスする唯一の方法では、アプリケーションの hive のルート キーを識別するハンドルを使用します。 アプリケーションからこのハンドルを取得する、 **RegLoadAppKey**ハイブをロードの呼び出し。

アプリケーションは、明示的に、アプリケーションのハイブをアンロードする必要はありません。 ハイブへのハンドルのすべてが終了した後、オペレーティング システムは自動的にアプリケーションのハイブをアンロードします。

アプリケーション、hive は、hive 内のキーにセキュリティ記述子の設定をサポートしていません。 代わりに、全体の hive の 1 つのセキュリティ記述子があります。 エラー状態の状態を使用しようとするアプリケーションの hive のキーのセキュリティ記述子を設定するのには失敗\_アクセス\_が拒否されました。 他の種類の各キーは、独自のセキュリティ記述子を使用してセキュリティで保護のレジストリ ハイブとは異なり、アプリケーションの hive のセキュリティは、hive ファイルのセキュリティ記述子に基づきます。 したがって、ハイブの読み込み中に成功しているエンティティは、全体の hive を変更できます。

レジストリのフィルター ドライバーへの呼び出しを受け取るその[ *RegistryCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ex_callback_function)アプリケーション ハイブのレジストリ操作の日常的な。 これらの呼び出しは、アプリケーション ハイブにおけるレジストリ操作とレジストリ ハイブの他の型に対する演算によって区別されません。 キーの作成とオープン キーの操作を処理するレジストリ フィルター ドライバー (で表示される、 **RegNtPreOpenKey**、 **RegNtPreOpenKeyEx**、 **RegNtPreCreateKey**、**RegNtPreCreateKeyEx**通知の値)、次の特殊な状況を正しく処理する必要があります。 アプリケーション、hive が読み込まれるときに、読み込みプロセスの最後のステップはレジストリ マネージャーでの hive のルート キーの開始にです。 レジストリ マネージャーは、キーは、パス名の文字列にすることを絶対パスでは、このオープン キー操作を発行、 **CompleteName**のメンバー、 [ **REG\_作成\_キー\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reg_create_key_information)、 [ **REG\_作成\_キー\_情報\_V1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reg_create_key_information_v1)、 [ **REG\_オープン\_キー\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560957)、または[ **REG\_オープン\_キー\_情報\_V1** ](https://msdn.microsoft.com/library/windows/hardware/ff560959)で開始されます。 構造体"\\レジストリ\\A\\"。 レジストリ マネージャーのみでは、絶対パスを使用して、アプリケーション、ハイブを開きます。 レジストリのフィルター ドライバーがこの方法で、アプリケーションの hive を確立しようとしたかどうか (など、呼び出すことによって、 [ **ZwOpenKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey)ルーチン)、エラーの状態で、操作は失敗\_へのアクセス\_拒否されました。

 

 





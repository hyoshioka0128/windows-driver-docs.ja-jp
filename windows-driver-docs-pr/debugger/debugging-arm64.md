---
title: ARM64 のデバッグ
description: ARM64 のデバッグ
keywords:
- ARM64 のデバッグ
- デバッグ
- ARM64
ms.date: 07/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 630230a2a8fc7de2ae616ef7ca9e541812257e86
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366934"
---
# <a name="debugging-on-arm64"></a>ARM64 でのデバッグ

このトピックでは、ARM プロセッサ上の Windows 10 のデバッグについて説明します。 ARM の Windows 10 の全般については、次を参照してください。 [ARM64 の Windows 10 デスクトップ](https://docs.microsoft.com/windows/uwp/porting/apps-on-arm)します。

一般に、ユーザー モードのアプリをデバッグする開発者は、バージョンの対象とするアプリケーションのアーキテクチャに一致するデバッガーを使用する必要があります。 WinDbg の ARM64 バージョンを使用して、ユーザー モード ARM64 アプリケーションをデバッグして、WinDbg の ARM バージョンを使用して、ユーザー モード ARM32 アプリケーションをデバッグします。 ARM64 プロセッサで実行されるユーザー モード x86 アプリケーションをデバッグする WinDbg のバージョンを x86 を使用します。  

WOW64 など CHPE – – システム コードをデバッグする必要があるまれなケースでは、WinDbg の ARM64 バージョンを使用できます。 別のコンピューターから ARM64 カーネルをデバッグする場合は、その他のコンピューターのアーキテクチャに一致する WinDbg のバージョンを使用します。  


## <a name="getting-arm--debugging-tools-for-windows"></a>ARM Windows 用デバッグ ツールの取得 

ことができますを取得するデバッグ ツール ARM64 をダウンロードして、 [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) (バージョン 10.0.16299 以降)。  インストール中、選択、*ツールを Windows のデバッグ*ボックス。 

デバッグ ツールがある、`Debuggers`キットのインストール ディレクトリ内のフォルダー。  ツールは、x86 `Debuggers\x86`、ARM32 ツールは、 `Debuggers\ARM`、ARM64 ツールと`Debuggers\ARM64`します。 

## <a name="debugging-arm64-code"></a>ARM64 コードのデバッグ

ARM64 コードをデバッグするには、ARM64 WinDbg が必要です。 デバッグ エクスペリエンスが x86 のデバッグとほぼ同じ x86 アプリケーション WinDbg x86 上で次の相違点を除いて、Windows。 

- Sp x0 に x28 と fp、lr、- 32 汎用レジスタがあります。 
- プログラム カウンター レジスタ、pc が汎用レジスタではありません。 
- すべての汎用レジスタし、pc レジスタは 64 ビット幅でします。 
- 最大で 2 アクティブなデータ用のブレークポイントの実行とメモリの読み取り/書き込みの 2 つのアクティブなデータ ブレークポイント。 詳細については、次を参照してください。[プロセッサ ブレークポイント](https://docs.microsoft.com/windows-hardware/drivers/debugger/processor-breakpoints---ba-breakpoints-)します。 


## <a name="debugging-x86-user-mode-code"></a>ユーザー モード コードの x86 のデバッグ 

ARM64 WinDbg を使用して、x86 をデバッグする必要があるまれなケースで、ユーザー モード コード コンテキストを切り替えるに次の WinDbg コマンドを使用することができます。 

- .effmach x86:切り替えと x86 を参照してくださいコンテキスト、x86 を使用しての効果をシミュレートする WinDbg します。 
- .effmach arm64:切り替えて、ARM64 コンテキストを参照してください。 
- .effmach chpe:切り替えて、CHPE コンテキストを参照してください。 

詳細については、.effmach を参照してください。 [.effmach (効果的な Machine)](-effmach--effective-machine-.md)します。

X86 をデバッグするときにアプリがユーザー モードに関係なく WinDbg のバージョンを使用しているが、これらの考慮事項に注意してください。

- スレッドがアクティブにデバッグされない場合 (シングル ステップ実行、ブレークポイントを検出しましたなど)、例外を報告していないシステムの呼び出しではなくレジスタのコンテキストが最新でないとします。 
- 内部的に、エミュレーターは、データ不整合、無効な命令、ページで I/O エラーの例外が生成され、生成するものを処理します。 WinDbg を使用しているときに、これらの例外として構成することを検討してください*は無視されます*デバッグ、イベントをフィルター処理しています. メニュー項目。  
- ARM64 WinDbg を使用して、ユーザー モードで、x86 & CHPE 関数の境界の間でシングル ステップ実行はサポートされません。 この問題を回避するには、対象のコードにブレークポイントを設定します。 

ARM64 および WOW64 の全般的な情報を参照してください。[を実行している 32 ビット アプリケーション](https://docs.microsoft.com/windows/desktop/WinProg64/running-32-bit-applications)64 ビット Windows プログラミング ガイド。 

WOW64 の下で実行されているアプリケーションをデバッグする方法の詳細については、次を参照してください。[デバッグ WOW64](https://docs.microsoft.com/windows/desktop/WinProg64/debugging-wow64)します。



## <a name="debugging-in-visual-studio"></a>Visual Studio でのデバッグ 

Visual Studio での ARM のデバッグ方法の詳細については、次を参照してください。[リモート デバッグ](https://docs.microsoft.com/visualstudio/debugger/remote-debugging)します。



## <a name="see-also"></a>参照

[WDK を使った ARM64 ドライバーのビルド](../develop/building-arm64-drivers.md)

[Windows コミュニティにスタンド アップ、常に接続されている PC の説明](https://blogs.windows.com/buildingapps/2018/01/22/windows-community-standup-discussing-always-connected-pc/)

-------







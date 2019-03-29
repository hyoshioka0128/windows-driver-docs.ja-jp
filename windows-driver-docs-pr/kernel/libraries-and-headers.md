---
title: ライブラリとヘッダー
description: ライブラリとヘッダー
ms.assetid: 0d4d0273-775f-4cbb-8b7f-63b22f3ccdae
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 849e879833c40eb06ac63562bbbae10185dd0ae0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572578"
---
# <a name="libraries-and-headers"></a>ライブラリとヘッダー


カーネル モード ドライバーでは、ネイティブ システム サービス ルーチンを使用して、呼び出すことによって、 **Nt**と**Zw** Ntoskrnl.exe ダイナミック リンク ライブラリ (DLL) 内のエントリ ポイント。 この DLL には、これらのルーチンの実際の実装が含まれています。 これらのエントリ ポイントにアクセスするには、ドライバーは Windows Driver Kit (WDK) で使用される Ntoskrnl.lib ライブラリに静的にリンクします。 Ntoskrnl.lib で実装されているルーチンでは、実行時に、Ntoskrnl.exe のエントリ ポイントに動的にリンク スタブがあります。

WDK ドキュメントでは、いくつかについて説明しますのすべてではありません、 **Zw** Ntoskrnl.exe 内のエントリ ポイント。 説明については、 **Zw**ドライバーによって呼び出すことができるルーチンを参照してください[ZwXxx ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff567122)します。

ドキュメントのほとんど**Zw**ルーチンは、WDK で Wdm.h ヘッダー ファイルで定義されているが、いくつかは Ntddk.h Ntifs.h などの他のヘッダー ファイルで定義します。

通常、ユーザー モード アプリケーションは呼び出しません、 **Nt**と**Zw**ルーチン。 代わりに、アプリケーションは可能性があります、Win32 のルーチンをなど、呼び出す[CreateFile](https://go.microsoft.com/fwlink/p/?linkid=152795)、しなど、ネイティブ システム サービス ルーチンの呼び出し[NtCreateFile](https://go.microsoft.com/fwlink/p/?linkid=157250)または[ **ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)を要求された操作を実行します。 ただし、ユーザー モード アプリケーションを呼び出すことがあります直接、 **Nt**または**Zw** Win32 ルーチンによってサポートされていない操作を実行するルーチン。

ユーザー モード アプリケーションでは、Ntdll.dll ダイナミック リンク ライブラリのエントリ ポイントを呼び出すことによって、ネイティブ システム サービス ルーチンを使用します。 これらのエントリ ポイントへの呼び出しを変換する**Nt**と**Zw**カーネル モードには、トラップ システム コールにルーチン。 これらのエントリ ポイントにアクセスするには、ユーザー モード アプリケーションは WDK で使用可能な Ntdll.lib ライブラリに静的にリンクします。 Ntdll.lib で実装されているルーチンでは、実行時に、Ntdll.dll のエントリ ポイントに動的にリンク スタブがあります。

Windows SDK のドキュメントでは、いくつかについて説明しますのすべてではありません、 **Nt** Ntdll.lib 内のエントリ ポイント。 ドキュメントのほとんど**Nt**ルーチンは、Windows SDK の Winternl.h ヘッダー ファイルで定義されます。 このドキュメントは、ほとんどのメンションの**Zw** 、エントリ ポイントとの定義を含む、Windows SDK でないヘッダー ファイル**Zw**ルーチン。

いくつかの小さな例外を各エントリ ポイントの Ntdll.dll で、 **Nt**ルーチンの一致するエントリ ポイントには、 **Zw**ルーチン。 WDK と Windows SDK のドキュメントでは、アプリケーション開発者が記載されていない呼び出しを避けることをお勧め**Nt**エントリ ポイント、および警告が表示されますが、 **Zw**で Ntdll.dll からエントリ ポイントが消える可能性があります、Windows の将来のバージョン。 アプリケーション開発者が呼び出す、 **Zw**この状況の発生をユーザー モードからのルーチンを準備する必要があります。

説明については、 **Nt** 、アプリケーションで呼び出すことができるルーチンを参照してください[Winternl](https://go.microsoft.com/fwlink/p/?linkid=157253)、[ファイル](https://go.microsoft.com/fwlink/p/?linkid=157254)、および[その他の低レベル クライアント サポート](https://go.microsoft.com/fwlink/p/?linkid=157255). 一部のページを参照**Nt** Windows sdk でルーチンは、「非推奨」ルーチンは、ラベルを付けるし、リーダーではなく、非推奨と等価の Win32 ルーチンを使用することをお勧め**Nt**ルーチン。

ユーザー モード アプリケーションが、Ntoskrnl.exe のエントリ ポイントを呼び出すことはできませんし、カーネル モード ドライバー Ntdll.dll のエントリ ポイントを呼び出すことはできません。

 

 





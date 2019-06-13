---
ms.assetid: 602bf657-7ae4-4610-b4c0-9d7260c42063
title: ドライバー パッケージの配布
description: ドライバー パッケージの配布
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1324c5771328a6a121554d1a4aa4bf803b09051a
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "64368617"
---
# <a name="distributing-a-driver-package"></a>ドライバー パッケージの配布

## <span id="ddk_distributing_a_driver_pg"></span><span id="DDK_DISTRIBUTING_A_DRIVER_PG"></span>


このトピックでは、ドライバー パッケージを安全に配布する方法について説明します。 Microsoft Windows Update プログラムを通じてドライバー パッケージを配布する方法についての情報も含まれています。 ここでは、Windows がシステム ファイルをどのように保護するかについても説明します。

## <a name="span-idddkwindowsupdatepgspanspan-idddkwindowsupdatepgspanwindows-update"></a><span id="ddk_windows_update_pg"></span><span id="DDK_WINDOWS_UPDATE_PG"></span>Windows Update


* [Windows ハードウェア認定キット (HCK)](https://msdn.microsoft.com/Library/Windows/Hardware/Ff544840) のテストに合格した[ドライバー パッケージ](https://go.microsoft.com/fwlink/p/?linkid=254893)は、WHQL でデジタル署名することができます。 ドライバー パッケージが WHQL によってデジタル署名されると、Windows Update プログラムや Microsoft がサポートする他の配布メカニズムによって配布することができます。

WHQL リリース署名の取得は、[Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893) の一部です。 WHQL リリース署名は、デジタル署名された[カタログ ファイル](https://msdn.microsoft.com/Library/Windows/Hardware/Ff537872)から成ります。 テスト向けに提出するドライバーのバイナリ ファイルや INF ファイルがデジタル署名によって変更されることはありません。

ドライバー パッケージが以下の条件を満たせば、Windows Update プログラムを通じてドライバー パッケージを配布できます。

-   WHQL テスト プログラムに合格し、[WHQL リリース署名](https://msdn.microsoft.com/Library/Windows/Hardware/Ff553976)を取得する。

-   Windows 認定プログラムの資格を得る。

-   Windows Update がユーザーのデバイスのための正しいドライバー パッケージを判断し、合法的に配布し、自動的にダウンロードできるようにするための追加の要件を満たす。

Windows Update プログラムの要件は頻繁に更新されるため、[Windows Update でのドライバーの公開](https://go.microsoft.com/fwlink/p/?linkid=8712)に関する Web サイトを定期的に確認する必要があります。

## <a name="span-idddkprotectionforsystemfilespgspanspan-idddkprotectionforsystemfilespgspanprotection-for-system-files"></a><span id="ddk_protection_for_system_files_pg"></span><span id="DDK_PROTECTION_FOR_SYSTEM_FILES_PG"></span>システム ファイルの保護


Windows ファイル保護 (WFP) では、Windows オペレーティング システム ファイルが不明なバージョンや互換性のないバージョンに置き換えられないように保護します。

重要な Windows システム ファイルがプログラムによって置き換えられることを防ぎます。 それらのファイルは、オペレーティング システムや他のプログラムによって使われるので、プログラムで上書きしないでください。 これらのファイルを保護することにより、プログラムとオペレーティング システムの問題を回避できます。

WFP が保護するシステム ファイルの種類は、オペレーティング システムに付属して提供される .sys、.exe、.ocx、.dll ファイルなどです。

WHQL テスト中に、[**Signability**](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089) プログラムによって、ドライバーの INF ファイルがシステム ファイルを置換しようとしないことが確認されます。 システム ファイルを置換しようとするドライバー パッケージは、デジタル署名を取得できません。 ただし、ドライバー パッケージには、Windows 2000 以降のバージョンのオペレーティング システムに同梱するためにベンダーが Microsoft に提供したファイルの更新されたバージョンを含めることはできます。

Windows ファイル保護に関する追加情報については、Windows SDK ドキュメントをご覧ください。

 

 






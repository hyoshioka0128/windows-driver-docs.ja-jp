---
title: サポートされているドライバー
description: サポートされているドライバー
ms.assetid: 1d41a9a9-415a-4dba-8b52-138c47ad63fd
keywords:
- Static Driver Verifier WDK、要件
- StaticDV WDK、要件
- SDV の WDK、要件
- 関数のプロトタイプ WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78811c4e2c1546efe7dc5f9feccfaec884c1102d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560022"
---
# <a name="supported-drivers"></a>サポートされているドライバー


ドライバーを確認する SDV のドライバーのコードを具体的には、解釈、ドライバーのエントリ ポイントできる必要があり、関数をサポートするルーチン内のコードに必要なドライバーの機能です。

次のセクションでは、ドライバーと SDV は、これを検証するドライバーが必要ですが、特定の構文の基本的な要件について説明します。 SDV は、ドライバーが場合、ドライバーが準拠していない、SDV を実行できない可能性があり、まれな状況で、結果を報告 false 正の値または false 負誤ってトライグラフとして解釈のため、これらの要件に従うことを確認できません。

### <a name="span-idbasicdrivercharacteristicsspanspan-idbasicdrivercharacteristicsspanbasic-driver-characteristics"></a><span id="basic_driver_characteristics"></span><span id="BASIC_DRIVER_CHARACTERISTICS"></span>基本的なドライバーの特性

SDV は、次の特性を持つドライバーのみを確認できません。

-   SDV は、ドライバーと C および C++ で記述されたライブラリを確認します。

-   SDV は、KMDF 対応および WDM 対応のデバイス ドライバー (関数ドライバー、フィルター ドライバー、バス ドライバー)、(フィルター、ミニポート、およびプロトコル ドライバー)、NDIS ドライバー、Storport ドライバーに対してだけ、完全な検証を実行します。

-   SDV は、汎用プロパティの制限付きの検証を試みます (など[NullCheck](nullcheckw.md)) 上記のカテゴリに適合しないドライバーにします。

-   SDV は、WDM 関数のロールの種類を使用して、ドライバーのコールバック関数を宣言する WDM ドライバーを確認できます。 関数を宣言する方法については、[を宣言する関数を使用して関数ロールの種類の WDM ドライバー](declaring-functions-using-function-role-types-for-wdm-drivers.md)を参照してください。

-   SDV はから生成されるドライバーを確認できます、[カーネル モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff544296)、SDV KMDF コールバック関数ロールの種類を使用して各コールバック関数を宣言します。 詳細については、[を使用して関数の役割の種類 KMDF ドライバーで関数を宣言する](static-driver-verifier-kmdf-function-declarations.md)を参照してください。

-   SDV は、SDV NDIS コールバック関数の型を使用して、関数宣言では、各コールバック関数に注釈を付ける提供される、NDIS ドライバーを確認できます。 詳細については、[を宣言する関数を使用してロール関数の種類の NDIS ドライバー](static-driver-verifier-ndis-function-declarations.md)を参照してください。

-   SDV は、関数の宣言では、各コールバック関数に注釈を付けること、Storport のドライバーを確認できます。 SDV Storport コールバック関数の型を使用してこれを行います。 詳細については、[を宣言する関数を使用してロール関数の種類 Storport ドライバー](declaring-functions-by-using-function-role-types-for-storport-drivers.md)を参照してください。

### <a name="span-idbasicdriverrequirementsspanspan-idbasicdriverrequirementsspanbasic-driver-requirements"></a><span id="basic_driver_requirements"></span><span id="BASIC_DRIVER_REQUIREMENTS"></span>基本的なドライバーの要件

WDM ドライバーを確認する SDV は、ドライバー必要があります。

- Wdm.h または Ntddk.h を含める (Wdm.h は Ntddk.h のサブセットです)。

- 記載されているメソッドを使用してデバイス オブジェクトを作成する[WDM デバイス オブジェクトとデバイス スタック](https://msdn.microsoft.com/library/windows/hardware/ff565639)します。

- 推奨されているように記述されたアンロード ルーチンがある[、アンロード ルーチンを記述](https://msdn.microsoft.com/library/windows/hardware/ff566400)します。

- 説明されている、関数の役割の型宣言を使用してディスパッチ関数は各宣言[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)します。 WDM ロールの種類については、 **\_ディスパッチ\_型\_(**<em>型</em>**)** 注釈、を参照してください[WDM ドライバーのロールの種類の関数を使用して関数の宣言](declaring-functions-using-function-role-types-for-wdm-drivers.md)します。

KMDF ドライバーを確認する SDV は、ドライバー必要があります。

-   Wdf.h Ntddk.h などがあります。

-   説明されている KMDF オブジェクトを作成する[ドライバーを開発するフレームワークを使用して](https://msdn.microsoft.com/library/windows/hardware/ff545545)します。

-   型を使用して、SDV KMDF コールバック関数の役割で説明されている各コールバック関数の注釈を付ける[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)します。 サポートされているロールの種類の一覧は、[静的ドライバー検証ツール KMDF 関数宣言](static-driver-verifier-kmdf-function-declarations.md)を参照してください。

SDV NDIS ドライバーを確認する、ドライバー必要があります。

-   Ndis.h Ntddk.h などがあります。

-   ガイドラインに従う、[ネットワーク設計ガイド](https://msdn.microsoft.com/library/windows/hardware/ff568356)NDIS ドライバーを作成します。

-   」の説明に従って、SDV NDIS コールバック関数の役割の型を使用して各コールバック関数に注釈を付ける[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)します。 サポートされているロールの種類の一覧は、[静的ドライバー検証ツールの NDIS 関数宣言](static-driver-verifier-ndis-function-declarations.md)を参照してください。

さらに、SDV は、サポートするドライバーを確認できます。

-   [プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)します。

-   [電源管理](https://msdn.microsoft.com/library/windows/hardware/ff547131)します。

-   [Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff547139) (WMI)。

### <a name="span-idreservedfunctionnamesspanspan-idreservedfunctionnamesspanreserved-function-names"></a><span id="reserved_function_names"></span><span id="RESERVED_FUNCTION_NAMES"></span>予約済みの関数名

SDV[検証エンジン](verification-engine.md)が正しく動作しないドライバーまたはライブラリ コードが内部的に使用して同じ関数名のパターンを使用する場合。

具体的には、SDV が正しく解釈されないコード場合。

-   コードに関数名で始まる\_ \_init とが続く 1 つ以上の整数など\_ \_init123 します。

-   コードには、sdv で始まる関数名が含まれています\_、sdv など\_Func、または文字列を含める\_sdv\_、Func など\_sdv\_または Func\_sdv\_ 。foo します。

-   ライブラリでは、.def ファイルを使用して、エクスポートされた関数の名前を変更して、外部の名前は、ライブラリ内の別の静的関数の名前と同じです。

ドライバーのコードまたはライブラリ コードは、これらの要素が含まれています、SDV は、ドライバーを確認します。 または、ライブラリを処理を試みますが、結果は場合**いないサポートされている機能 (NSF)** します。 SDV の結果の詳細については、[静的ドライバー検証結果を解釈する](interpreting-static-driver-verifier-results.md)を参照してください。

 

 






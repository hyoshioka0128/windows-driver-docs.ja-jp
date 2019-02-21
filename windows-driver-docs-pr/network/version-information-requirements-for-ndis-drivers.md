---
title: NDIS ドライバーのバージョン情報の要件
description: NDIS ドライバーのバージョン情報の要件
ms.assetid: a05e7dde-d1f9-458d-8d7b-ead9bb9af7af
keywords:
- NDIS バージョン情報 WDK、NDIS 責任
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564854aa86a18b009113be468e8505afddaa544f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527291"
---
# <a name="version-information-requirements-for-ndis-drivers"></a>NDIS ドライバーのバージョン情報の要件





バージョン情報を提供する NDIS 構造体が、**ヘッダー**メンバーとして定義されている、 [ **NDIS\_オブジェクト\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566588)構造体および NDIS ドライバーは、このようなバージョン情報のサポートを提供する必要があります。

NDIS はより高いまたは低い NDIS バージョンをサポートするドライバーをサポートできる、*現在のバージョンの NDIS* (つまり、NDIS、コンピューターが実行されているオペレーティング システムのバージョンでサポートされているのバージョン)。 また、*登録済みのバージョンの NDIS* (ドライバーが初期化中に報告されたバージョン) のドライバーはドライバーがサポートする最上位バージョンより低くすることができます。 たとえば、NDIS 6.1、NDIS 5.1 ドライバーは、NDIS 6.0 を実行しているオペレーティング システムのバージョンで実行できます。 5.1 の NDIS ドライバーは、単に、初期化中に、5.1 の NDIS ドライバーとして登録します。 ただし、NDIS 6.1 ドライバーは、NDIS の現在のバージョンを確認する必要があります、(この例では、NDIS 6.0) で提供される NDIS の最高レベルをサポートしているドライバーとして登録する必要があります。 現在の NDIS バージョンを取得する方法の詳細については、次を参照してください。 [NDIS バージョンを入手](obtaining-the-ndis-version.md)します。

**注**  ドライバーは、構造体の新しいバージョンのすべての機能をサポートする必要はありません。 たとえば、ミニポート ドライバーは、バージョン 2 の構造を作成し、バージョン 1 の構造体の適切な値を指定します。

 

バージョン情報を保持する構造内のメンバーにアクセスするには、NDIS ドライバーは、次のプロセスを完了する必要があります。

-   チェック、 **Header.Revision**と**Header.Size**構造体のメンバーにアクセスする前にメンバー。

-   以前のバージョンの構造 (つまり、ドライバーをサポートする NDIS バージョンに関連付けられている数よりも低いリビジョン番号を持つ構造)。
    -   ドライバーは、ことを確認する必要があります、 **Header.Size**で値が正しく、 **Header.Revision**値。 たとえば、NDIS の値\_SIZEOF\_Xxx\_リビジョン\_1 は Xxx の正しい\_リビジョン\_1 が小さすぎるため Xxx\_リビジョン\_2。
    -   **Header.Size** NDIS 以上の値がある必要があります\_SIZEOF\_Xxx\_リビジョン\_Nn (場所*Nn*のリビジョン番号が、ドライバーを使用している構造) と、ドライバーがそのリビジョンに適切な構造体の情報を正しく処理する必要があります。
-   以降のバージョン構造 (つまり、ドライバーをサポートする NDIS バージョンに関連付けられている数よりも上位のバージョン番号を保持する構造) の場合、ドライバーは、構造体の以前のバージョンの場合と同様、構造体を使用できます。 高いバージョンの構造は、以前のバージョンと互換性が常に。

-   ドライバーは、ドライバーの登録済みの NDIS バージョンの構造体の正しいバージョンを使用する必要があります。 たとえば、NDIS 6.1 ドライバーが内でのオフロード機能をレポートする必要があります[ **NDIS\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566599)構造体メンバーを設定して、 [ **NDIS\_オブジェクト\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566588)構造を示す NDIS\_オフロード\_リビジョン\_2。 ただし、ドライバーが NDIS に含まれているすべての機能をサポートする必要ありません\_オフロード\_リビジョン\_2。

-   OID のセット要求を正常に処理するドライバーを設定する必要があります、 **SupportedRevision**内のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)OID のセットの要求からの戻り時に構造体。 **SupportedRevision**メンバーのリビジョン、ドライバーがサポートされている要求の発信側に通知します。 たとえば、ミニポート ドライバーが、Xxx を作成できます\_リビジョン\_2 構造、および、Xxx の適切な値を指定\_リビジョン\_1 の構造、およびゼロの構造体の残りの部分の塗りつぶし。 ミニポート ドライバーの Xxx は報告\_リビジョン\_で 1、 **SupportedRevision**メンバー。 ここで、Xxx をサポートできるプロトコル ドライバー\_リビジョン\_2 が Xxx を使用して\_リビジョン\_ミニポート ドライバーがサポートされている 1 つの情報。

-   どのような情報が、基になるドライバーが正常に処理を確認するのに OID 要求を発行するドライバーに関連する必要があります値をチェック、 **SupportedRevision** NDIS でメンバー\_OID\_要求OID 要求が返された後に構造体。

## <a name="related-topics"></a>関連トピック


[NDIS のバージョンの概要](overview-of-ndis-versions.md)

[NDIS バージョン情報を指定します。](specifying-ndis-version-information.md)

 

 







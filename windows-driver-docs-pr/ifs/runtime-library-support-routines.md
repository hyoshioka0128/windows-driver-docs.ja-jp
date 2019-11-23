---
title: ランタイムライブラリのサポートルーチン
description: ランタイムライブラリのサポートルーチン
ms.assetid: e333a222-32c0-46e7-a0b8-42287e19372d
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: b4c20fac746e3d55374ec6039a52907878281095
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955804"
---
# <a name="runtime-library-support-routines"></a>ランタイムライブラリのサポートルーチン

次の表は、システムによって提供されるランタイムライブラリサポートルーチンのうち、カーネルモードのファイルシステムで使用できるものと、ミニフィルターとレガシフィルタードライバーによって使用されるものの、デバイスドライバーによるものではないものを示しています。

ここに記載されているルーチンに加えて、ファイルシステムとフィルタードライバーは、 *ntifs*で宣言されているカーネルモードドライバーアーキテクチャリファレンスセクションで説明されている**Rtl**_Xxx_ルーチンを呼び出すこともできます。

**ヘッダーファイル:** *ntifs*

**プレフィックス: Rtl**_Xxx_

| 関数またはマクロ | 説明 |
| ----------------- | ----------- |
| **RtlAbsoluteToSelfRelativeSD** | 絶対形式のセキュリティ記述子をテンプレートとして使用して、自己相対形式で新しいセキュリティ記述子を作成します。 |
| **RtlAddAccessAllowedAce** | アクセス許可のアクセス制御エントリ (ACE: access control list) をアクセス制御リスト (ACL) に追加します。 指定されたセキュリティ識別子 (SID) へのアクセスが許可されます。 |
| **RtlAddAccessAllowedAceEx** | アクセス許可のアクセス制御エントリ (ACE) を継承 ACE フラグと共にアクセス制御リスト (ACL) に追加します。 指定されたセキュリティ識別子 (SID) へのアクセスが許可されます。 |
| **RtlAddAce** | 指定したアクセス制御リスト (ACL) に1つ以上のアクセス制御エントリ (Ace) を追加します。 |
| **RtlAllocateAndInitializeSid** | システム用に予約されています。 |
| **RtlAllocateHeap** | ヒープからメモリブロックを割り当てます。 |
| **RtlAppendStringToString** | 2つのカウントされた文字列を連結します。 コピー元からコピー先のバッファーの長さまでバイトをコピーします。 |
| **RtlCaptureContext** | 呼び出し元のコンテキストでコンテキストレコードを取得します。 |
| **RtlCaptureStackBackTrace** | スタックをウォークし、各フレームの情報を記録することによって、スタックバックトレースをキャプチャします。 |
| **RtlCompareMemoryUlong** | 指定したパターンに一致するメモリブロック内のバイト数を返します。 |
| **Rtlの圧縮 Sbuffer** | は、バッファーを圧縮し、ファイルシステムドライバーがファイルの圧縮の実装を容易にするために使用できます。 |
| **RtlCompressChunks** | システム用に予約されています。 |
| **RtlConvertSidToUnicodeString** | セキュリティ識別子 (SID) の印刷可能な Unicode 文字列形式を生成します。 |
| **RtlCopyLuid** | ローカル一意識別子 (LUID) をバッファーにコピーします。 |
| **RtlCopySid** | セキュリティ識別子 (SID) の値をバッファーにコピーします。 |
| **RtlCreateAcl** | アクセス制御リスト (ACL) を作成して初期化します。 |
| **RtlCreateHeap** | 呼び出しプロセスで使用できるヒープオブジェクトを作成します。 このルーチンは、プロセスの仮想アドレス空間の領域を予約し、このブロックの指定した初期部分に物理記憶域を割り当てます。 |
| **RtlCreateSecurityDescriptorRelative** | 自己相対形式で新しいセキュリティ記述子を初期化します。 返されると、セキュリティ記述子は、システム ACL (SACL)、随意 ACL (DACL)、所有者、プライマリグループ、およびすべての制御フラグがゼロに設定された状態で初期化されます。 |
| **RtlCreateSystemVolumeInformationFolder** | ファイルシステムボリュームに "システムボリューム情報" フォルダーが存在することを確認します。 フォルダーが存在しない場合は、フォルダーが作成されます。 |
| **RtlCreateUnicodeString** | 新しいカウントされた Unicode 文字列を作成します。 |
| **RtlCustomCPToUnicodeN** | システム用に予約されています。 |
| **RtlDecompressBuffer** | 圧縮バッファー全体を圧縮解除します。 |
| **RtlDecompressBufferEx** | 圧縮バッファー全体を圧縮解除します。 |
| **RtlDecompressBufferEx2** | 可能な限り複数のプロセッサを使用して、圧縮バッファー全体を圧縮解除します。 複数のプロセッサのサポートは、カーネルモードの呼び出し専用に実装されています。 |
| **RtlDecompressChunks** | システム用に予約されています。 |
| **RtlDecompressFragment** | 圧縮されたバッファーの一部 (つまり、バッファー "fragment") の圧縮を解除します。 |
| **RtlDecompressFragmentEx** | 可能な限り複数のプロセッサを使用して、圧縮されたバッファーの一部 (つまり、バッファー "fragment") を圧縮解除します。 |
| **RtlDelete** | 指定されたノードを s リンクツリーから削除します。 |
| **RtlDeleteAce** | 指定したアクセス制御リスト (ACL) からアクセス制御エントリ (ACE: access control entry) を削除します。 |
| **Rtldele/Osplay** | 指定されたノードを s リンクツリーから削除します。 |
| **RtlDeleteElementGenericTable** | ジェネリックテーブルから要素を削除します。 |
| **RtlDeleteElementGenericTableAvl** | ジェネリックテーブルから要素を削除します。 |
| **RtlDescribeChunk** | システム用に予約されています。 |
| **RtlDestroyHeap** | 指定したヒープオブジェクトを破棄します。 | \* * RtlDestroyHeap デとは、プライベートヒープオブジェクトのすべてのページを解放し、ヒープへのハンドルを無効にします。 |
| **RtlDowncaseUnicodeString** | 指定した Unicode ソース文字列を小文字に変換します。 変換は、現在のシステムロケール情報に準拠しています。 |
| **RtlEnumerateGenericTable** | ジェネリックテーブル内の要素を列挙します。 |
| **RtlEnumerateGenericTableAvl** | ジェネリックテーブル内の要素を列挙します。 |
| **RtlEnumerateGenericTableLikeADirectory** | ジェネリックテーブルの要素を1つずつ照合順序で返します。 |
| **RtlEnumerateGenericTableWithoutSplaying** | ジェネリックテーブル内の要素を列挙します。 |
| **RtlEnumerateGenericTableWithoutSplayingAvl** | ジェネリックテーブル内の要素を列挙します。 |
| **RtlEqualPrefixSid** | 2つのセキュリティ識別子 (SID) プレフィックスが等しいかどうかを判断します。 SID プレフィックスは、最後の subauthority 値を除く SID 全体です。 |
| **RtlEqualSid** | 2つのセキュリティ識別子 (SID) の値が等しいかどうかを判断します。 2つの Sid は、等しいと見なされるために正確に一致する必要があります。 |
| **RtlFillMemoryUlong** | 指定されたメモリ範囲に、ULONG 値の1回以上の繰り返しを格納します。 |
| **RtlFillMemoryUlonglong** | 指定した ULONGLONG 値の1回以上の繰り返しを使用して、指定した範囲のメモリを塗りつぶします。 |
| **RtlFindUnicodePrefix** | プレフィックステーブルで、指定した Unicode ファイル名に最も一致するものを検索します。 |
| **RtlFreeHeap** | **Rtlallocateheap**によってヒープから割り当てられたメモリブロックを解放します。 |
| **RtlFreeOemString** | Rtl. によって割り当てられたストレージを解放します **。ToOemString**ルーチン。 |
| **RtlFreeSid** | システム用に予約されています。 |
| **RtlGenerate8dot3Name** | 指定された長いファイル名の短い (8.3) 名前を生成します。 |
| **RtlGetAce** | アクセス制御リスト (ACL) 内のアクセス制御エントリ (ACE: access control entry) へのポインターを取得します。 |
| **RtlGetCompressionWorkSpaceSize** | **RtlRtlDecompressFragment Sbuffer**関数と関数のワークスペースバッファーの正しいサイズを決定します。 |
| **RtlGetDaclSecurityDescriptor** | セキュリティ記述子の随意 ACL (DACL) へのポインターを返します。 |
| **RtlGetElementGenericTable** | 特定のジェネリックテーブル要素について、呼び出し元から提供されたデータへのポインターを返します。 |
| **RtlGetElementGenericTableAvl** | 特定のジェネリック Adelson-Velsky/Landis (AVL) テーブル要素について、呼び出し元から提供されたデータへのポインターを返します。 |
| **RtlGetGroupSecurityDescriptor** | 指定されたセキュリティ記述子のプライマリグループ情報を返します。 |
| **RtlGetOwnerSecurityDescriptor** | 指定されたセキュリティ記述子の所有者情報を返します。 |
| **RtlGetSaclSecurityDescriptor** | セキュリティ記述子のシステム ACL (SACL) へのポインターを返します。 |
| **RtlIdentifierAuthoritySid** | システム用に予約されています。 |
| **RtlInitCodePageTable** | システム用に予約されています。 |
| **RtlInitializeGenericTable** | 汎用テーブルを初期化します。 |
| **RtlInitializeGenericTableAvl** | Adelson-Velsky/Landis (AVL) ツリーを使用して汎用テーブルを初期化します。 |
| **RtlInitializeSid** | セキュリティ識別子 (SID) 構造体を初期化します。 |
| **Rtlinitializeside x** | 事前に割り当てられたセキュリティ識別子 (SID) 構造体を初期化します。 |
| **RtlInitializeSplayLinks** | S リンクノードを初期化します。 |
| **RtlInitializeUnicodePrefix** | プレフィックステーブルを初期化します。 |
| **RtlInsertAsLeftChild** | S リンクノードを、指定されたノードの左側の子としてツリーに挿入します。 |
| **RtlInsertAsRightChild** | 指定された s リンクをツリー内の特定のノードの右側の子としてツリーに挿入します。 |
| **RtlInsertElementGenericTable** | ジェネリックテーブルに新しい要素を追加します。 |
| **RtlInsertElementGenericTableAvl** | ジェネリックテーブルに新しいエントリを追加します。 |
| **RtlInsertElementGenericTableFullAvl** | ジェネリックテーブルに新しいエントリを追加します。 |
| **RtlInsertUnicodePrefix** | 新しい要素を Unicode プレフィックステーブルに挿入します。 |
| **RtlIsGenericTableEmpty** | ジェネリックテーブルが空かどうかを判断します。 |
| **RtlIsGenericTableEmptyAvl** | ジェネリックテーブルが空かどうかを判断します。 |
| **RtlIsLeftChild** | 指定された s リンクが s リンクツリー内のノードの左側の子であるかどうかを判断します。 |
| **RtlIsNameLegalDOS8Dot3** | 指定した名前が有効な短い (8.3) ファイル名を表しているかどうかを判断します。 |
| **RtlIsRightChild** | 指定された s リンクが s リンクツリー内のノードの右側の子であるかどうかを判断します。 |
| **RtlIsRoot** | 指定したノードが s リンクツリーのルートノードであるかどうかを判断します。 |
| **RtlIsValidOemCharacter** | 指定した Unicode 文字を有効な OEM 文字にマップできるかどうかを判断します。 |
| **Rtll 子** | 指定された s リンクノードの左側の子へのポインターを返します。 |
| **RtlLengthRequiredSid** | 指定された数のサブ機関を持つセキュリティ識別子 (SID) を格納するために必要なバッファーの長さをバイト単位で返します。 |
| **RtlLengthSid** | 有効なセキュリティ識別子 (SID) の長さをバイト単位で返します。 |
| **RtlLookupElementGenericTable** | 指定されたデータに一致する要素を汎用テーブルで検索します。 |
| **RtlLookupElementGenericTableAvl** | 指定されたデータに一致する要素を汎用テーブルで検索します。 |
| **RtlLookupElementGenericTableFullAvl** | 指定されたデータに一致する要素を汎用テーブルで検索します。 |
| **RtlLookupFirstMatchingElementGenericTableAvl** | 指定されたデータに一致するツリー内の左端の要素を検索します。 |
| **RtlMultiByteToUnicodeN** | 現在のシステム ANSI コードページ (ACP) を使用して、指定されたソース文字列を Unicode 文字列に変換します。 ソース文字列は、必ずしもマルチバイト文字セットのものではありません。 |
| **RtlMultiByteToUnicodeSize** | 指定されたソース文字列の Unicode 翻訳を格納するために必要なバイト数を決定します。 翻訳は、現在のシステム ANSI コードページ (ACP) を使用することを前提としています。 ソース文字列は、必ずしもマルチバイト文字セットのものではありません。 |
| **RtlNextUnicodePrefix** | Unicode プレフィックステーブル内の要素を列挙します。 |
| **RtlNtStatusToDosError** | 指定した NTSTATUS コードを、それと等価なシステムエラーコードに変換します。 |
| **RtlNtStatusToDosErrorNoTeb** | システム用に予約されています。 |
| **Rtlnumber Generictableelements** | ジェネリックテーブル内の要素の数を返します。 |
| **Rtlnumber Generictableelementsavl** | ジェネリックテーブル内の要素の数を返します。 |
| **RtlOemStringToCountedUnicodeSize** | 指定された OEM 文字列を、カウントされた Unicode 文字列に変換した後の、バイト単位のサイズを決定します。 |
| **RtlOemStringToCountedUnicodeString** | 現在のシステムの OEM コードページを使用して、指定されたソース文字列を Unicode 文字列に変換します。 |
| **RtlOemStringToUnicodeSize** | Null で終わる Unicode 文字列に変換された後の、指定された OEM 文字列のサイズ (バイト単位) を決定します。 |
| **RtlxOemStringToUnicodeSize** | システム用に予約されています。 |
| **RtlOemStringToUnicodeString** | 現在のシステムの OEM コードページを使用して、指定されたソース文字列を null で終わる Unicode 文字列に変換します。 |
| **RtlOemToUnicodeN** | 現在のシステムの OEM コードページを使用して、指定されたソース文字列を Unicode 文字列に変換します。 |
| **RtlOffsetToPointer** | 指定されたベースアドレスからの特定のオフセットに対するポインターを返します。 |
| **RtlParent** | S リンクツリー内の指定されたノードの親へのポインターを返します。 |
| **Rtlポインタ Tooffset** | 指定されたポインターの指定したベースアドレスからのオフセットを返します。 |
| **RtlRandom** | 指定されたシード値から生成された乱数を返します。 |
| **RtlRandomEx** | 指定されたシード値から生成された乱数を返します。 |
| **RtlRealPredecessor** | S リンクツリー内の指定されたノードの先行するポインターを返します。 |
| **RtlRealSuccessor** | S リンクツリー内の指定されたノードの後続のノードへのポインターを返します。 |
| **RtlRemoveUnicodePrefix** | プレフィックステーブルから要素を削除します。 |
| **RtlReserveChunk** | システム用に予約されています。 |
| **Rtlall 子** | 指定された s リンクノードの右の子へのポインターを返します。 |
| **RtlSecondsSince1970ToTime** | 1970の先頭から絶対システム時刻の値までの経過時間を秒単位で変換します。 |
| **RtlSecondsSince1980ToTime** | 1980の先頭から絶対システム時刻の値までの経過時間を秒単位で変換します。 |
| **RtlSelfRelativeToAbsoluteSD** | 自己相対形式のセキュリティ記述子をテンプレートとして使用して、絶対形式で新しいセキュリティ記述子を作成します。 |
| **RtlSetGroupSecurityDescriptor** | 絶対形式のセキュリティ記述子のプライマリグループ情報を設定します。 これにより、セキュリティ記述子に既に存在する主要なグループ情報が置き換えられます。 |
| **RtlSetOwnerSecurityDescriptor** | 絶対形式のセキュリティ記述子の所有者情報を設定します。 このメソッドは、セキュリティ記述子に既に存在するすべての所有者情報を置き換えます。 |
| **RtlSplay** | 指定された s リンクの周りに s リンクツリーを作成し、そのリンクをツリーの新しいルートにバランスます。 |
| **RtlSubAuthorityCountSid** | システム用に予約されています。 |
| **RtlSubAuthoritySid** | セキュリティ識別子 (SID) の指定された subauthority へのポインターを返します。 |
| **RtlSubtreePredecessor** | そのノードをルートとするサブツリー内の指定されたノードの先行するへのポインターを返します。 |
| **Rtlsubtreesucまたは** | そのノードをルートとするサブツリー内の指定されたノードの後続の位置へのポインターを返します。 |
| **RtlTimeToSecondsSince1970** | 指定した絶対システム時刻の値を、1970の先頭以降の経過時間 (秒単位) に変換します。 |
| **RtlTimeToSecondsSince1980** | 指定した絶対システム時刻の値を、1980の先頭以降の経過時間 (秒単位) に変換します。 |
| **RtlUnicodeStringToAnsiSize** | 指定した Unicode 文字列の ANSI 変換を格納するために必要なバイト数を決定します。 |
| **RtlUnicodeStringToCountedOemString** | 現在のシステムの OEM コードページを使用して、指定した Unicode ソース文字列を、カウントされた OEM 文字列に変換します。 |
| **RtlUnicodeStringToOemSize** | 指定された Unicode 文字列を OEM 文字列に変換した後のバイト単位のサイズを決定します。 |
| **RtlUnicodeStringToOemSize** | システム用に予約されています。 |
| **RtlUnicodeStringToOemString** | 現在のシステムの OEM コードページを使用して、指定された Unicode ソース文字列を OEM 文字列に変換します。 |
| **RtlUnicodeToCustomCPN** | システム用に予約されています。 |
| **RtlUnicodeToMultiByteN** | 現在のシステム ANSI コードページ (ACP) を使用して、指定した Unicode 文字列を新しい文字列に変換します。 翻訳された文字列は、必ずしもマルチバイト文字セットのものではありません。 |
| **RtlUnicodeToMultiByteSize** | 指定した Unicode 文字列のマルチバイト変換を格納するために必要なバイト数を決定します。 翻訳は、現在のシステム ANSI コードページ (ACP) を使用することを前提としています。 |
| **RtlUnicodeToOemN** | 現在のシステムの OEM コードページを使用して、指定された Unicode 文字列を OEM 文字列に変換します。 |
| **RtlUpcaseUnicodeStringToCountedOemString** | 現在のシステムの OEM コードページを使用して、指定された Unicode ソース文字列を大文字で計算された OEM 文字列に変換します。 |
| **RtlUpcaseUnicodeStringToOemString** | 現在のシステムの OEM コードページを使用して、指定された Unicode ソース文字列を大文字の OEM 文字列に変換します。 |
| **RtlUpcaseUnicodeToCustomCPN** | システム用に予約されています。 |
| **RtlUpcaseUnicodeToMultiByteN** | 現在のシステム ANSI コードページ (ACP) を使用して、指定した Unicode 文字列を新しい大文字の文字列に変換します。 翻訳された文字列は、必ずしもマルチバイト文字セットのものではありません。 |
| **RtlUpcaseUnicodeToOemN** | 現在のシステムの OEM コードページを使用して、指定された Unicode 文字列を大文字の OEM 文字列に変換します。 |
| **RtlValidSid** | リビジョン番号が既知の範囲内であり、サブ機関の数が最大値未満であることを確認することによって、セキュリティ識別子 (SID) を検証します。 |

---
layout: post
title: "개츠비 스타터 블로그: Twitter 카드 지원으로 게시물에 헤더 이미지를 추가하는 방법"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2020/12/freeCodeCamp-GatsbyBlogImageTwitterCard-5.png
tags: undefined
---


저와 같다면, 개츠비 스타터 블로그를 이용해서 개인 블로그를 시작하고, 몇 가지 커스터마이징을 한 다음, 그 블로그와 함께 롤링을 했습니다.

마크다운 형태의 새로운 게시물을 추가하는 것은 멋진 일입니다. 하지만 코드를 볼 이유가 거의 없다는 뜻이기도 합니다. 그래서 제가 트위터 카드를 지원하면서 제 게시물에 헤더 이미지를 추가하기로 결정했을 때, 저는 상실감을 느꼈습니다.

제 요구 사항은 다음과 같이 캡션이 있는 대형 헤더 이미지를 게시물에 추가할 수 있어야 했습니다.

또한 게시물에 대한 링크가 포함된 트윗은 다음과 같이 큰 이미지가 있는 트위터의 요약 카드로 "확장"되어야 합니다.

마지막으로 이미지를 지정하지 않은 게시물의 경우 트위터의 요약 카드를 사용하여 기본 이미지를 표시해야 합니다. 다음은 웹 사이트 로고를 기본 이미지로 사용한 위치입니다.

참고: Twitter의 문서에는 카드 이미지에 웹 사이트 로고를 사용하면 안 된다고 명시되어 있습니다(여기 `트위터:이미지` 섹션 참조). 제가 여기 있는 것처럼 고정된 이미지를 예비로 사용하는 것이 타당한지 판단하도록 하겠습니다.

## 시작하기

다음은 제가 안내해 드릴 다섯 가지 고급 단계입니다. 모든 것을 자세히 설명하고 도중에 다른 리소스에 대한 링크를 제공하겠습니다. 그렇게 하면 개츠비에 대한 지식을 쌓을 수 있고, 그 지식을 바탕으로 나중에 더 복잡한 단계를 해결할 수 있습니다.

- 문서 메타데이터 태그 추가
- 그래프를 사용한 원본 기본 이미지QL
- 그래프를 사용한 원본 사후 특정 이미지 속성QL
- 블로그 포스트 템플릿에 헤더 이미지 추가
- 게시물의 앞부분에 새 속성 추가

우리가 이 모든 것을 성취하기 위해 사용할 도구들은 개츠비 스타터 블로그와 함께 개봉됩니다!

- 대응 헬멧 - `SEO` 구성 요소에서 트위터 카드 및 기타 개방형 그래프 태그를 지원하기 위해 문서 헤드에 메타 태그를 추가하는 데 사용됩니다.
- 개츠비 소스 파일 시스템 - "로컬 파일 시스템에서 개츠비 응용 프로그램에 데이터를 소싱하기 위한 플러그인", 우리의 경우 이미지
- 개츠비 이미지 - "개츠비의 그래프QL 쿼리와 원활하게 작동하도록 특별히 설계된 리액트 컴포넌트입니다. 개츠비의 기본 이미지 처리 기능과 고급 이미지 로딩 기술을 결합하여 사이트에 대한 이미지 로드를 쉽고 완전하게 최적화합니다. 이미지 변신에 힘을 실어주기 위해 개츠비 이미지.
- 개츠비 플러그인 샤프 - "샤프 이미지 처리 라이브러리에 구축된 여러 이미지 처리 기능을 노출합니다." 이미지 크기를 조정할 때 사용합니다.

## 문서 메타데이터 태그를 추가하는 방법

먼저, Twitter에서 읽을 수 있는 HTML 메타데이터 태그와 Google, Facebook, WhatsApp과 같은 Open Graph를 이해하는 다른 플랫폼 또는 툴들을 연결할 것이다.

문서 메타데이터에 대한 자세한 내용은 여기를 참조하십시오. 머리에 뭐가 있지? HTML의 메타데이터입니다.

`src/components/seo.js`에서 `SEO` 구성 요소를 엽니다. 가장 먼저 주목해야 할 점은 리액트 헬멧을 사용하고 있으며 이미 og:title, twitter:description과 같은 많은 오픈 그래프와 트위터 메타 태그를 보유하고 있다는 점이다. 요약 값이 `twitter:card` 태그도 있어 이미지가 없는 기본 트위터 요약 카드를 사용할 수 있다.

```undefined
// src/components/seo.js
const SEO = ({ description, lang, meta, title }) => { 
// Details omitted for brevity 
return ( 
    <Helmet 
        htmlAttributes={ lang } 
        title={title} 
        titleTemplate={`%s | ${site.siteMetadata.title}`} 
        meta={[ 
            { name: `description`, content: metaDescription, }, 
            { property: `og:title`, content: title, }, 
            { property: `og:description`, content: metaDescription, }, 
            { property: `og:type`, content: `website`, }, 
            { property: `twitter:card`, content: `summary`, }, 
            { property: `twitter:creator`, 
              content: site.siteMetadata.social.twitter, }, 
            // ...
```

이 구성 요소를 업데이트하겠습니다.

- imageUrl 및 image 추가Alt ` 매개 변수. 이것들은 나중에 볼 수 있듯이 `블로그 포스트 템플릿` 컴포넌트에서 소품으로 전달될 것이다. 프로필 이름에 "URL"을 사용하여 완전한 URL이어야 한다는 사실을 전달했습니다. OG 이미지에는 상대 경로가 지원되지 않습니다!
- 기본 이미지 URL인 `defaultImageUrl`을 구성합니다. 기본 URL과 상대 경로를 연결하기 위해 작은 유틸리티 함수인 constructUrl을 작성했습니다. 다음 섹션에서 data.ogImageDefault의 출처를 확인할 수 있습니다.
- imageSrcUrl 프로포즈를 사용하는 ogImageUrl 변수를 추가합니다(제공되지 않은 경우). 기본값은 defaultImageUrl입니다).
- Helmet 구성 요소인 og:image, twitter:card 및 twitter:image:alt에 전달된 `meta` 배열에 개체 추가

여기서 주의해야 할 몇 가지 사항:

- 트위터에는 자체적인 `트위터:이미지` 메타 태그가 있지만, 문서에 따르면, 우리는 트위터의 파서가 다시 오픈 그래프 태그로 돌아갈 것이기 때문에 `og:image`와 `twitter:image` 태그를 둘 다 추가할 필요가 없다.
- 오픈그래프는 메타 속성 및 콘텐츠 속성을 지정하고, 트위터는 이름 및 콘텐츠를 각각 지정한다. 그러나, 트위터 문서들은 그들의 파서가 오픈 그래프 속성으로 되돌아갈 것이라고 말한다. 이는 일관성을 유지할 수 있고 동기화해야 하는 동일한 값의 반복 속성이 필요하지 않기 때문에 좋습니다.
- 메타 태그에 속성 속성을 사용할 경우 예외적으로 `이름` 특성을 사용해야 하는 설명과 같이 열려 있지 않은 그래프 태그가 있습니다. 나는 당신이 당신의 SEO에 대한 기본적인 문제들을 확인할 수 있는 Lighthouse를 사용하는 것을 추천합니다.

```undefined
// util.js
export const constructUrl = (baseUrl, path) =>
  (!baseUrl || !path) ? null : `${baseUrl}${path}`;

// src/components/seo.js
// Step 1: Add props
const SEO = ({ description, lang, meta, title, imageUrl, imageAlt }) => { 
    
    const data = useStaticQuery(
        // This is explained next
    );
                                
    // Step 2: Construct default image URL
    // ogImageDefault is explained next
    const defaultImageUrl = constructUrl(data.site.siteMetadata.siteUrl, data.ogImageDefault?.childImageSharp?.fixed?.src)
    
    // Step 3: Add this
    const ogImageUrl = imageUrl || defaultImageUrl; 
    
    return ( 
        // Step 4: Add new meta objects
        <Helmet 
            htmlAttributes={ lang } 
            title={title} 
            titleTemplate={`%s | ${site.siteMetadata.title}`} 
            meta={[
                { property: `og:image`, content: ogImageUrl, }, 

                // If a post has an image, use the larger card. 
                // Otherwise the default image is just 
                // a small logo, so use the smaller card.
                { property: `twitter:card`, content: imageUrl ? `summary_large_image` : `summary`, }, 

                // Add image alt text
                // Falls back to default which describes the site logo
                { property: `twitter:image:alt`, content: imageAlt || "davidagood.com logo", }, 
                // ...
```

## 그래프를 사용하여 기본 이미지를 원본화하는 방법QL

여기서 개츠비의 파일 시스템과 이미지 처리 능력이 발휘된다. 아래는 `SEO` 구성 요소의 `usseStaticQuery` 호출 GraphQL 쿼리입니다. 위에 나와 있는 constructUrl 통화에 필요한 ogImageDefault 부분과 siteUrl 부분을 추가하였습니다.

```undefined
// src/components/seo.js
const data = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
            description
            social {
              twitter
            }
            # Add this
            siteUrl
          }
        }
        # Add this
        ogImageDefault: file(relativePath: {eq: "icon.png"}) { 
          childImageSharp {
            fixed(height: 260, width: 260) {
              src
            }
          }
        }
      }
    `,
);
```

### 그래프QL 파일 및 이미지 처리 쿼리 설명

최상위 노드는 `ogImageDefault`입니다. 이것은 필터를 적용하여 상대 경로가 `icon.png`인 파일을 찾는 `file` 쿼리의 GraphQL 별칭입니다. 제가 선택한 `ogImageDefault`라는 이름은 완전히 임의적입니다.

여기서 이해해야 할 한 가지 핵심 사항은 상대 경로가 어떤 상대 경로인지에 대한 것이다. 다시 말해 icon.png라는 파일이 어디에 있는가.

먼저 프로젝트 루트와 관련된 파일의 위치를 알려드리겠습니다: `/content/assets/icon.png`. 쿼리에서 상대 경로를 지정하지 않고 파일 이름만 지정했습니다. 그러면 개츠비는 어떻게 그것을 어디서 찾아야 하는지 알 수 있을까요?

gats by source-filesystem을 입력한다. Gats by-config를 보면.js"와 같은 구성이 표시됩니다.

```undefined
// gatsby-config.js 
module.exports = { 
    // siteMetadata: {...}, 
    plugins: [ 
        // Other plugins omitted 
        { 
            resolve: `gatsby-source-filesystem`, 
         options: { 
                path: `${__dirname}/content/blog`, 
                name: `blog`, 
            }, 
        }, 
        { 
            resolve: `gatsby-source-filesystem`, 
            options: { 
                path: `${__dirname}/content/assets`, 
                name: `assets`, 
            }, 
        }, 
     // ...
```

이 작업은 이러한 경로를 "콘텐츠 루트"로 등록하고 이름을 지정하는 것입니다. 따라서 블로그라는 이름은 프로젝트 루트를 기준으로 한 컨텐츠/블로그를 의미합니다. 그리고 `자산`이란 명칭은 프로젝트 루트와 관련된 `//콘텐츠/자산`을 의미한다. sourceInstanceName에서 필터링하여 쿼리에서 다음 이름을 사용할 수 있습니다.

```undefined
# http://localhost:8000/___graphql 
{ 
    allFile(filter: {sourceInstanceName: {eq: "blog"}) { 
        edges { 
            node { 
                absolutePath 
                publicURL 
                sourceInstanceName 
            } 
        } 
    } 
}
```

이 쿼리의 결과:

```undefined
// Result of allFiles query with sourceInstanceName filter 
{ 
    "data": { 
        "allFile": { 
            "edges": [{ 
                "node": { 
                    "absolutePath": "/home/dgood/IdeaProjects/davidagood.com/content/blog/clean-code-and-architecture/index.md", 
                    "publicURL": "/static/40bb02d938c4faf7f977dd66c1a399d2/index.md", 
                    "sourceInstanceName": "blog" 
                } 
            }, 
            // additional results...
```

ogImageDefault로 돌아가서, 우리가 제공한 `상대 경로`는 `icon.png`에 불과했지만, 실제로 파일은 `/content/assets/icon.png`에 있습니다.

Gatsby가 파일을 해결할 수 있었던 것은 "//content/assets"에서 "콘텐츠 루트"를 구성했기 때문입니다. 원본 인스턴스 이름을 지정하여 이 파일이 위치한 "콘텐츠 루트"에 대한 모호성을 제거할 수 있었습니다.

사실, 나는 만약 같은 상대적인 경로가 여러 "콘텐츠 루트"에 존재한다면 개츠비가 어떻게 행동할지 잘 모르겠다.

이 모든 일이 어떻게 진행되는지 이해하기 위해 개츠비의 소스 코드를 파헤칠 수 있는 좋은 기회가 되겠지만, 그건 당신에게 맡기겠어요!

다음으로, `차일드 이미지 샤프`란 무엇인가? "Child"는 파일 노드의 하위 노드라고 합니다. "이미지"는 들리는 것과 똑같습니다. 샤프(Sharp)는 이러한 이미지 처리 기능을 가능하게 하는 샤프 이미지 처리 툴과 그에 상응하는 개츠비 플러그인-샤프를 가리킨다.

fixed(고정)는 이미지를 고정 크기의 이미지로 변환하는 것을 의미합니다. 우리는 다음과 같은 매개 변수를 전달하여 치수를 지정한다: `고정(높이: 260, 너비: 260). 우리가 사용할 수 있는 `고정`에 대한 몇 가지 대안이 있는데, 그 중 하나는 우리가 아래에서 보게 될 것이다.

마지막으로, 우리는 오픈 그래프 이미지 메타 태그의 목적을 위한 `src` 속성만 필요하다.

## 그래프를 사용하여 특정 이미지 속성을 소싱하는 방법QL

위에서 `imageUrl`과 `imageUrl`을 전달하기 위해 `BlogPostTemplate` 구성 요소를 업데이트해야 합니다.Alt는 SEO 구성 요소를 소품합니다. 다시, 우리는 상대적 경로인 `src`를 URL로 변환하기 위해 `constructUrl` 유틸리티를 사용한다. 나는 아래에서 이러한 소품 값의 출처를 설명한다.

```undefined
// util.js
export const constructUrl = (baseUrl, path) =>
  (!baseUrl || !path) ? null : `${baseUrl}${path}`;

// src/templates/blog-post.js
const BlogPostTemplate = ({ data, pageContext, location }) => { 
    // Details omitted for brevity
    return ( 
        <Layout location={location} title={data.site.siteMetadata.title}> 
            <SEO 
                title={data.markdownRemark.frontmatter.title} 
                description={data.markdownRemark.frontmatter.description || data.markdownRemark.excerpt} 
                imageUrl={
                    constructUrl(
                        data.site.siteMetadata.siteUrl, data.markdownRemark.frontmatter.image?.childImageSharp?.fixed?.src
                )} 
                imageAlt={data.markdownRemark.frontmatter.imageAlt} />
        // ...
```

이미지 alt 텍스트 소싱은 간단합니다. 이미지를 추가합니다.Alt는 BlogPostTemplate 구성 요소의 GraphQL 쿼리에서 `전면 물질` 부분에 대한 속성입니다. 이 쿼리는 GraphQL 태그가 지정된 템플릿으로 내보냅니다.

내보낸 상수의 이름은 임의입니다. 내 경우 `const pageQuery`입니다.

이 쿼리는 개츠비에 의해 실행되며, 결과는 데이터 소품에서 BlogPostTemplate 구성 요소로 전달됩니다.

이것은 Gatsby의 문서: GraphQL로 페이지의 데이터 질의에서 설명된다.

실제 이미지를 소싱하기 위해 ChildImageSharp을 다시 사용하지만 위에서 본 것과는 약간 다른 방식으로 사용합니다.

```undefined
// src/templates/blog-post.js
export const pageQuery = graphql`
    query BlogPostBySlug($slug: String!) {
      site {
        siteMetadata {
          title
          siteUrl
        }
      }
      markdownRemark(fields: {slug: {eq: $slug}) {
        id
        excerpt(pruneLength: 160)
        html
        frontmatter {
          title
          date(formatString: "MMMM DD, YYYY")
          description
          # Add this
          image {
            childImageSharp {
              fixed(height: 600, width: 1200) {
                src
              }
              fluid(maxWidth: 700, maxHeight: 500) {
                ...GatsbyImageSharpFluid
              }
            }
          }
          # Add these
          imageAlt
          imageTitleHtml
        }
      }
    }
`;
```

여기서 `이미지`는 우편물 앞부분에 설정하려는 부동산의 이름과 일치해야 한다. 그리고 이 속성의 값은 포스트 마크다운 파일과 관련된 파일 경로여야 합니다.

이것은 우리가 GraphQL 별칭과 파일 쿼리를 사용하여 위에서 했던 것과 유사하지만, 여기서는 암시적으로 개츠비에 의해 배후에서 처리되고 있다.

우리는 매개 변수에서 `고정` 필드에 치수를 지정한다. 치수를 선택할 때 사용하는 이미지가 여기서 지정한 치수 이상인지 확인하고 문서의 다음 지침을 사용하십시오.

> 이 카드의 이미지는 최소 300x157 또는 최대 4096x4096픽셀의 가로 세로 비율을 2:1로 지원합니다.

우리는 또한 `fluid` 속성과 GraphQL 조각 `...`을 추가했다.GatsbyImageSharpFluid`는 이 노드에서 사용할 수 있는 모든 속성을 하나씩 열거할 필요 없이 검색합니다.

개츠비 이미지 컴포넌트는 HTML의 기본 대응 이미지 기능을 사용하여 대응적인 이미지 경험을 제공하기 위해 이러한 방식으로 사용하도록 설계되었다.

## 블로그 포스트 템플릿에 헤더 이미지를 추가하는 방법

GraphQL 쿼리가 업데이트되고 개츠비가 결과를 컴포넌트로 전달함에 따라, 우리는 헤더 이미지와 캡션을 위한 JSX와 Gatsby 이미지 가져오기를 추가할 준비가 되었다.

```undefined
// src/templates/blog-post.js
import Image from "gatsby-image";

// Details omitted for brevity

{data.markdownRemark.frontmatter.image?.childImageSharp?.fluid &&
    <>
        <Image
            fluid={data.markdownRemark.frontmatter.image.childImageSharp.fluid}
            alt={data.markdownRemark.frontmatter.imageAlt} 
        />
        <div
            style={
                textAlign: "center",
                fontSize: "14px",
                lineHeight: "28px",
            }
            dangerouslySetInnerHTML={ 
                __html: data.markdownRemark.frontmatter.imageTitleHtml 
            } 
        />
     <br/>
        <br/>
    </>
}
```

`이미지` 또는 `이미지`인 경우알트의 성질은 우편물 앞부분에서 정해진 것이 아니라 아무런 문제도 일으키지 않을 것이다. 이러한 속성은 게시물의 데이터 소자(예: data.markdownRemark.frontmatter.image), data.markdownRemark.imageAlt와 같은 데이터 소자(data.markdownRemark.frontmatter.imageAlt)에 "null"로 표시됩니다.

이러한 이유로, 나는 `imageUrl` 소품을 `SEO` 구성 요소인 `data.markdownRemark.frontmatter.image?`에 전달할 때 선택적 체인을 사용해 왔다.아이 이미지 샤프?fixed?src 및 헤더 이미지 구성 요소 트리(`data.markdownRemark.frontmatter.image?)를 선택적으로 추가하는 경우.아이 이미지 샤프?액체의

## 게시물의 정면에 새 속성을 추가하는 방법

이제 실제 이미지 파일을 추가하는 일만 남았습니다. 일반적으로 이 파일을 사용할 마크다운과 같은 디렉터리에 말이죠. 그런 다음 이미지, 이미지를 추가합니다.Alt 및 `image`게시물의 앞부분에 Html 속성을 지정합니다.

Unsplash에서 직접 추천 속성 HTML을 가져와 `이미지`에 사용했습니다.제목Html"입니다.

이 경우 이미지 경로는 포스트 마크다운 파일에 상대적입니다.

```undefined
--- 
title: "Working with Heterogeneous Item Collections in the DynamoDB Enhanced Client for Java" 
date: "2020-12-07T01:51:34.815Z"
description: "Working with heterogeneous item collections with the Java SDKs can be tricky. Here we see how to handle 
them with the AWS SDK v2 for Java's Enhanced Client."
image: "./kevin-mueller-gGUiw8GNIFE-unsplash.jpg"
imageAlt: "Water droplets on black background"
imageTitleHtml: '<span>Photo by <a href="https://unsplash.com/@kevinmueller?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Kevin Mueller</a> on <a href="https://unsplash.com/?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>'

--- 

// Markdown here...
```

## 결론

바로 그거야! 해냈어! 우리는 이 글에서 꽤 많은 개념을 다루었다. 이제 블로그 게시물에 헤더 이미지를 추가하고 Twitter, Facebook, Google, WhatsApp 등에서 멋진 Open Graph 기반 미리 보기 경험을 얻을 수 있습니다.

완료된 코드는 GitHub에서 확인할 수 있습니다.

- 서
- 블로그 포스트 템플릿
- 사후 마크다운 예

이 기능을 구현하고 배포한 후에는 Twitter Card Validator를 사용하여 실제로 링크를 트윗하기 전에 동작을 테스트할 수 있습니다.

공교롭게도, 저는 검증자가 작동 중인 것으로 표시했음에도 불구하고 트윗에 카드가 표시되지 않는 몇 가지 문제를 경험했습니다.

한 가지 경우, 제가 트위터에 답글을 올렸는데 카드가 전혀 없었어요. 원시 링크만요. 다음 날, 같은 링크를 트위터에 올렸는데, 이번에는 카드가 잘 작동했어요!

또 다른 경우, 저는 제 트위터 프로필 페이지를 보고 있었는데, 제 트윗 중 몇 개가 카드를 가지고 있었지만 이미지가 표시되지 않았습니다. 그래서 저는 Chrome Incognito 창을 열었고, 그 창에는 예상대로 영상이 표시됩니다.
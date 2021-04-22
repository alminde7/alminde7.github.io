---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
permalink: /
---
 
 # Welcome  
 
 Hello hello

 ```csharp
 public class ReverseProxyHttpsRedirection
    {
        private const string ForwardedProtoHeader = "X-Forwarded-Proto";
        private readonly RequestDelegate _next;

        public ReverseProxyHttpsRedirection(RequestDelegate next)
        {
            _next = next;
        }

        public async Task Invoke(HttpContext ctx)
        {
            var headers = ctx.Request.Headers;
            if (headers[ForwardedProtoHeader] == string.Empty || headers[ForwardedProtoHeader] == "https")
            {
                await _next(ctx);
            }
            else if (headers[ForwardedProtoHeader] != "https")
            {
                var withHttps = $"https://{ctx.Request.Host}{ctx.Request.Path}{ctx.Request.QueryString}";
                ctx.Response.Redirect(withHttps);
            }
        }
    }

    public static class ReverseProxyHttpsRedirectionExtensions
    {
        public static IApplicationBuilder UseReverseProxyHttpsRedirection(this IApplicationBuilder builder)
        {
            return builder.UseMiddleware<ReverseProxyHttpsRedirection>();
        }
    }
 ```

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">
        {{ post.title }}
      </a>
      - <time datetime="{{ post.date | date: "%Y-%m-%d" }}">{{ post.date | date_to_long_string }}</time>
    </li>
  {% endfor %}
</ul>
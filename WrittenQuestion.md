The site already has some features in place such as pagination that will help it hold up under load but there are still 
several steps that could be taken to optimise it further.

# Backend Notes

Use keyset pagination instead of offset-based pagination.\
Offset becomes increasingly slow as the dataset grows. Keyset pagination scales better for large tables.

Add indexes on frequently filtered columns such as `tag_name` to keep filter and sort queries efficient.

Consider returning a more lightweight article object for the list page.
The current API returns full `ArticleDetails` for list endpoints. A dedicated lightweight DTO reduces payload size and improves response time.

Consider exposing useful metadata to the frontend
by including fields like `totalPages` and `articlesCount` which could be used to optimize pagination and navigation.

# Frontend Notes

Consider infinite scrolling with lazy loading 
instead of page-by-page navigation, articles can load progressively as the user scrolls to improve the UX.
If making this change we should also implement virtual scrolling which
prevents rendering hundreds of DOM nodes at once, this should improve the UI performance on large feeds.

Add local caching of fetched pages this avoids repeat network requests when navigating between pages or returning to previously viewed content.
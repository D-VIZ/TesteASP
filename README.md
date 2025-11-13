#teste

namespace ProjetoASP.Pages.Movies
{
    public class IndexModel : PageModel
    {
        private ProjetoASPContext _context;

        public IndexModel(ProjetoASPContext context)
        {
            _context = context;
        }

        public IList<Movie> Movies { get;set; } = new List<Movie>();

        [BindProperty(SupportsGet = true)]
        public string? SearchString { get; set; }

        public async Task OnGetAsync()
        {
            var movies = from m in _context.Movie select m;

            if (!string.IsNullOrWhiteSpace(SearchString))
            {
                movies = movies.Where(s => s.Title.Contains(SearchString));
            }

            Movies = await movies.ToListAsync();

        }

    }
}

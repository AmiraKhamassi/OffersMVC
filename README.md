// steps 
1- Vaut mieux commencer par créer header.php, index.php, style.css, et functions.php 



/****** To start with header.php *******/

<!DOCTYPE html>
<html lang="fr">
<head>
	<title>
		<?php bloginfo('name') ?>
		<?php if ( is_404() ) : ?> &raquo; 
		<?php _e('Not Found') ?>
			<?php elseif ( is_home() ) : ?> &raquo; 
				<?php bloginfo('description') ?>
			<?php else : ?>
				<?php wp_title() ?>
			<?php endif ?>
	</title>
 
	<meta http-equiv="Content-Type" content="<?php bloginfo('html_type'); ?>; charset=<?php bloginfo('charset'); ?>" />
	<meta name="generator" content="WordPress <?php bloginfo('version'); ?>" />
	<link rel="stylesheet" href="<?php bloginfo('stylesheet_url'); ?>" type="text/css" media="screen" />
	<?php wp_get_archives('type=monthly&format=link'); ?>
	<?php //comments_popup_script(); // off by default ?>
	<?php wp_head(); ?>
 
</head>
<body>
	<div id="page">
		<div id="header">
			<h1><a href="<?php bloginfo('url'); ?>"><?php bloginfo('name'); ?></a></h1>
			<?php bloginfo('description'); ?>
		</div>
    
    
/***** Then index.php *******/

<?php get_header(); ?>

	<div id="content">
		<?php if(have_posts()) : ?>
			<?php while(have_posts()) : the_post(); ?>
				<div class="post" id="post-<?php the_ID(); ?>">
					<div class="imageList">
						<?php
							if (has_post_thumbnail()) {
								the_post_thumbnail('thumbnail');
							}
						?>
					</div>
					<a href="<?php the_permalink(); ?>" title="Lire article"><?php the_title('<h2>','</h2>'); ?></a>
					<!-- postmetada-->
					<p class="postmetadata">
						Par: <?php the_author(); ?> | Le <?php the_time('j F Y'); ?> | Dans: <?php the_category(', '); ?>
						| <?php comments_popup_link(); ?>
					</p>
					<?php the_excerpt(); ?>
				</div>
			<?php endwhile; ?>
		<?php endif; ?>
	</div>
	<?php
		get_sidebar();
	?>

	<?php
		get_footer();
		wp_footer(); 
	?> 
</div><!--Fin de id_page-->

</body>
</html>
	
/***** Then style.css ****/

/***** functions.php *****/
Avec des le depert add_theme_support('post-thumbnails'); 
